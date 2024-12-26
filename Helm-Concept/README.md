```
:::HELM:::
	Helps ease deployment and lifecycle managment of application deployed on a Kubernetes cluster.
	works as a package/release manager, with install/uninstall wizard, help us to upgrade/rollback applications.
	it treat k8 apps as app instead of just a collection of obj.(no need to micro manage each and every obj)
	Obj:-
		Arch, Comp (Charts, repo, releases, revisions), writing charts, templating, functions, piplines, 
		conditionals, with block, Raange, Chart hooks, chart tests, provenance, Packaging&Signing, uploading,
		
==========================================
What/Why/ is helm?
	Kubernetes is good at managing complex infra, app that we deploy in k8's clusters can become very complicated.
	a app is usually made up of a collection of obj that need to interconnect to make everything work.
	ex:- simple app requires
		Deployment, services, Persiesnt volume, persistence volume claim, store(secret) , (backup, job ...so on)
		for every obj we need seperate YAMl file and apply those and make sure of connection b/w obj, and 
		what if we need to modify some thing in yaml, we need to go back to the file and need to do necessary edits what if it is a repetative task? and what if mess with some thing wrong?
	K8's doesn't really care about our app as a whole, it only know that we declear various obj, and it proceeds to make of them exist in our cluster
	it dosen't know that this is PV and that deployment and that secret store, service are all part of simple app,, it will take care individually.

	To address this issues 'HELM'
	Package manager for k8's, it looks those obj as part of a big package as a group, while performa a action, me only mention a package(simple app) not for the individual objects.
	Ex:-
	let's take game app in playstore, game consist of lot of things(music, graphic, ..so on) to run the app 
	we don't want to install all those seperately we get a gamm installer, we run it, we choose the dir to install and done.	
	Helm also doing the similar thing and more for the k8 objects.
	single cmd to install our entire app, even if their is thousands of objects.
	it automatically add every necessary obj to k8 without bothering us with details, 
	we can customize the settings we want for our app or package by specifing desired values at install time, but instead of having to edit, 
	we have a single location where we can declare every custom settings in a file like "values.yaml".
	We can upgrade/rollback with single cmd
==========================================
Helm 2 vs 3

	In Helm2:
		CLI client installed inlocal machiane helps to helm specific actions aganist k8 cluster, 
		lack of RBAC, and custom resource defination, 
		to work properly, 'tiller' had to be installed in the k8 cluster,
		whenever user want to perform a helm specific operations, our helm client communicated with tiller that was running on server, 
		tiller will communicate with k8 and processed to take actions to make req happen.(middleman).
		some security concerns, by default tiller is in god mode(had privileges to do anything wanted) (not good for all the user to have adminaccess)
		
		dosen't support 3-way strategic merge patch(only looks at revision not on chart and  current state)
		explain:-
		let's assume		
		install >> new revison added as revision 1(revision is nothing but snapshot)
		upgrade >> revision 2
		rollback >> create a new revision as revision 3 and compare revision 2 with revision 1 and make the necessary changesand finally 
		 made revison 3 (doesn't goes back to revision 1, but all the config as same as revision 1)
		senario:
			install >> revision 1
			upgrade done by manually by the user in k8's not through helm, then this update doesn't consider as new revision, 
			and then did rollback what happens?
			we have only one revision of the helm, it comapre with the old one,  so their is no change
		
	In Helm3:
		CLI client installed inlocal machiane helps to helm specific actions aganist k8 cluster, 
		No tiller, 
		RBAC, custom resource defination support,
		whatever RBAC permissions of k8 users we have same applicable to helm as well,(restrict the user by specific access to do the task)
		support 3-way stratehic merge patch.(looks at revision, on chart and current state)
		explain:
		same senario as above:
		it compares the chart currently in use if we had created a revision that is which we didn't the chart we want to revert to. 
		and alsothe live state how our k8 obj currently looks like their declaration in yamol form.
		by also looking live state, it notice the image version
==========================================
::Components::
	has multiple components we'll be working,
		charts are collection of files, contains all the instructions that helm needs to know to be able to create the collection of objects that you need in our k8 cluster.
		by using chart and adding the obj, acc to the specific instruction in the chart, Helm in a way installs application into cluster, when chart is appllied to cluster a new release is created.
		release is a single installation of an application using helm chart. each release we have multiple revisions/snapshot of application.
		every time a change is made to app(ie., upgrade of image or chnage of replicas or configuration a new revision is created....
		to keep track of what did in cluster(release, chart used, revision state ...so on) helm will need to place a save data(METADATA),
		helm is storing metadata in k8 cluster secrete, so that authorized user has access, and know the exact status,   
		
		We have lot of chart avalible in internet we can directly download and use it but the main thing is 
		values.yaml(setting file or input file for helm), it is where the defination chnages as per the application, we can customize as our own.
		
		when a chat is applied a release is created,
		helm install my-site-1 bitnami/wordpress
		make sure to give name, why?,  we can install multiple release based on the same chart. 
		so we can lauch a second app with a command,
		helm install my-site-2 bitnami/wordpress		
		two release they are seperate and have their own revisions, and tracked seperately and changes independently. even though they are based on same chart.
		
		helm repo has lot of charts to deploy as a new chart, let's say deploy redis or prometheus goes to helm repo and install those.
		helm repo comes into picture.
		lot of charts are already avaliable at different helm repo
		providers of helm repo are appscode, truecharts, bitnami, community operatores >> all this repo,chart are located in artifacthub.io
==========================================
:::HELM Charts:::
	HELM easy to use command line tool,(automation tool), but how it knows to do the task, by using charts.
	charts are like instructions manual for it. By reading and intrepreting the content, it then knows exactly ehat it has to do to fulfill a user's request.
	chart.yaml >> it contains info about chart itself, 
	chart structure:
		templates/ >> template directory
		value.yaml >> config values
		chart.yaml >> chart info
		license
		readme
		charts/ >> dependency chart.
==========================================
::cutomize chart parameters::
while installing we can customize chart parameters, 
1. by using 'set' option
	helm install --set .. --set .. <> <>
	
2. create cusom.yaml file and add all these and pass while installling.
	helm install --values <yamlfile>

3. break install into 2 cmds, 
	1.pull the chart
		helm pull <> >> pull in archive/compress form
		helm pull --untar <>
	2. then we ahve files and then edit our necessary things and 
	now run install but give the local path that we have edited yaml file.
==========================================
::Lifecycle Managment in HELM::
	each time we pull in a chart and install it, a new release will created(release similar to app, but more specific it represent a package or a collections of k8 objs)
	sincel heml know what k8 obj are relate to release, it can do things like upgrade, downgrade or uninstalls without touching obj that might belong to other release.
	each release can be managed independently, even aif they all based on same chart
	
	BY using rollback the data won't be backedup or restored.
	
==========================================
Writing a files, 
Nothing much just add the deploy.yaml and service.yaml files int he helm telplate directory and make sure the no static definations in the file, 
everthying has to be taken from values.yaml for custom.yaml or directly from the helm but no static definations.
reason, 
	if deployment name is static, we will release a chart by using that deployment, if want to again deploy the chart release from the same deployment file,
it through an error telling that chart is deployment is already there, so we can't reuse it, for that sake we always prefer template rendering(dynamic)  
		
what if you defined and forget to pass the value in values.yaml ?
ex: image: ____, then we need some default values.
in deployment.yaml fiel we can use {{default "nginx" ......}}

funtions:
 default
 upper ex;- {{ upper.Values.image.repository }}
 quote.
 replace.
 shuffle. ..and so on refer doc

Pipeline:
  {{ Values.image.repository | upper | quote | .. }}

conditionals:

Blocks:
	no need to metion everytime, simple like a scope, if this ".Values.app." is a app level scope no need to metion each and every argument, 
	we can simple use this
	instead we can use 
	{{- with .Values.app}}
	....
	{{- end }}
	Now want if we want to use from the root level inside the app scope simple use "$"

Ranges:
	nothing but loops.
	{{- range.Values.regions }}
	-{{ . | quote }}
	{{- end }}
	
Named Templates:
TEMPLATE ACTION
INCLUDE FUNCTION
	
	to remove duplication, re-use code,
	create _helpers.tpl in the template directory(where depoly and services files are here)
	all files start with '_' are skiped by helm while converted into a k'8 manifest file.
	in _helpers.tpl we can start with this
	{{- define "lables" }}
	 app.k8's.io/name : nginx
	{{- end }}
	and we can simple use this by {{- template "lables" }} in our deploy.yaml/service.yaml file
	if you use '.' in {{- template "lables" . }} then we can make dynamic from helper file as well
		{{- define "lables" }}
		app.k8's.io/name: .Release.Name
		{{- end }}
	
	Make sure same indentation across all the files, to make intedentation properly we can use "{{- include "lables" . | indent 2}}", 
	

:::CHART HOOKS:::
before our cmd execute, we need to do some thing before,
ex: use rollback, before the cmd execute, we need to store the data db backup, 
or else sending email before and after, 
these extra actions are implemented know as hooks
ex:-
	in general:
		helm upgrade >> verify >> render >> upgrade 
	by using hooks
	 helm upgrade >> verify >> render >> (pre-upgrade) >> upgrade >> (post upgrade)
	 helm upgrade >> verify >> render >> (pre-install) >> upgrade >> (post install)
	 helm upgrade >> verify >> render >> (pre-delete) >> upgrade >> (post delete)
	 helm upgrade >> verify >> render >> (pre-rollback) >> upgrade >> (post rollback)

to run continuosly we create a pod (kind = pod)
to trigger we use job, (kind = job)
so k8 obj pods and jobs that we configure hooks in helm charts.
so create a job.yaml file and keep this in templates folder hellm will take care of it.
but we need to tell that it is pre or post process, it is not a general yaml file, for that we use "annotations"
Annotations are a way for us to add additional metadata to an object which may be used by client of k8 in this case helm to store data about that obj and perform some kind of actions.

we add annotations with "helm.sh/hook" and values as pre-upgrade, 
what if multiple pre-upgrade hooks configure? ex:email, backup, so email first and backup next,
we can set weights to each other to priortize

:::Packaging and signing charts:::
to package >> helm package <path>
upload to chart repo,
	1st we need to sign in, and then upload, 
	crypto graphy security >>>  private key only chart developer have access with this key digital signature produces provenance file, 
	now whoever download the files, must have public key, 
		
==========================================
:::CMD:::
	helm version
	helm --help
	helm install <release-name> <chart-url>


	helm search (hub or repo) wordpress
	
Deploy app in two commds:
	helm repo add <repo-name> <repo-url>
	helm install <release-name> <path-to-local-chart>
or
	helm install <release-name> <repo-name>/<chart-name>
	
	
	helm repo update
	
	helm upgrade <release-name> <chart-name> [flags]
	
	helm list >> to get all the relaese
	
	helm uninstall <release_name> >> to delete the release
	
	helm history <chart_name>

	helm rollback <release-name> <revision-number>
	
	helm uninstall <release_name>
	
	helm package <path>

```
