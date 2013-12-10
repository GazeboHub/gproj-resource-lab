Resource Laboratory Framework - Gazebo Project
==============================================

> "Above all else, JCR is a programming interface for Java (and other JVM Programmatic API languages) to interact with content repositories independently from how those repositories are implemented."
>
> -- ModeShape Guide, section _What are repositories good at?_

> "CORBA models distributed resources as objects that provide a well-defined interface. [...] Since the transfer syntax for sending messages to objects is strictly defined, it is possible to exchange requests and replies between processes running programs written in arbitrary programming languages and hosted on arbitrary hardware and operating systems."
>
> -- JacORB 3.1 Programming Guide, section 1.1, _A Brief CORBA introduction_


## History

The GProj Recource Lab _work area_ was initialized for purpose of extending on an _abstract workspace_ concept denoted in the _README_ file of the _GProj  Shared Project Management Resources_ Work Area, as codified in the [gproj-project-manage][gproj-project-manage] _source tree_. In summary, the [gproj-project-manage][gproj-project-manage] source tree was designed so as to serve as a _shared submodule_ of GProj projects, initially in a context of projects using Git _submodules_ in addition to a submodule representing the [gproj-project-manage][gproj-project-manage] _source tree_. The [gproj-project-manage][gproj-project-manage] _source tree_, in itself, provides a public domain Git _hook_ script for purpose of preventing a _synzhronization error_, such as would be possible in the workflow of a project using Git _submodules_. That _source tree_ may provide further shared resources for GProj development - such as for sharing of convenient _external tool definitions_ for use in the [Eclipse IDE][eclipse].

In order to define a reproducible structure for managing a set of projects in developing the GProj web presence, within the [gproj-project-manage][gproj-project-manage] project, a _workspace_ model was defined such that that _workspace model_ may be introduced into the _SCCM information space_, with a _source tree_, `gproj-web-workspace`. The initial goal in defining that _workspace as source tree_ model was to ensure the [gproj-project-manage][gproj-project-manage] _source tree_ may be used _exactly once_, as a  _submodule_ in parallel to two existing source trees that would also be used as Git _submodules_ to that _workspace as source tree_ - namely, the `gproj-ghub-site-manage` and `portal-gproj-manage` source trees. Each of those source trees utilizes an additional submodule comprising, respectively, primarily _static_ web content and a submodule comprising an [OpenShift][oso] _application_. This results in essentially a _"multi-tier"_, _nested submodule_ model in the root source tree, as illustrated in the following _tree structure_.

* `gproj-web-workspace` , a _workspace as source tree_
    * `gproj-project-manage`, a _shared resources bundle_
    * `gproj-ghub-site-manage`, a _work area_, managing static content for the [GProj IO site][gproj-io] site, as hosted under _[GitHub Pages][ghPages]_
        * `gazebohub.github.io` containing the publishable content of the site, as a submodule
    * `portal-gproj-manage`, a _work area_, providing a `.war` file overlay customizing an upstream `.war` file, such that the upstream file provides the [Liferay][liferay] portal framework, centrally
        * `portal`, an [OpenShift][oso] _application_ comprised of [JBoss AS7][jbossas] and a [PostgreSQL][postgres] database, the application entailing some configuration of [JBoss AS7][jbossas] _modules_, the database's SQL _schemas_, and [OpenShift][oso] _hooks_, and as such, using a "push to deploy" model onto [OpenShift Online][osonline].

Furthermore, a seventh _source tree_ _shall be_ organized as a submodule in the `gproj-web-workspace`, namely [`archetype-oo-servlet-manage`][archetype-oo-servlet-manage], a project defining a [Maven][mvn] _archetype_ for purpose of creating a project structured such as `portal-gproj-manage` -- as for the generic situation of installing an upstream _Java web application_, with customizations in a formar of JAR file _overlays_, such that the customized files would be installed directly or indirectly into a _servlet container_ provided via an [OpenShift][oso] _application_.  The `archetype-oo-servlet-manage` _source tree_ would not utilize any Git _submodules_, itself, and may be managed as a further _submodule_ of the `gproj-web-workspace` _source tree_.


## Generalization of the "Source Tree as Workspace" Model

The _"Source tree as workspace"_ model instance, as denoted in the above, may be observed for applicability in a sense of a practical _pattern_ - as towards a development of an _information model_ with discrete _parameters_ for its instantiation, as such, if not towards the development of any more formal structures of [OMG UML][uml] models, including _UML diagrams_, as extensible via _UML profiles_, and in regards to broader _MOF metamodels_ such as [SysML][sysml].

This document shall propose, in rhetorical form, a generalization of the "Source Tree as Workspace" model, towards developing a platform-agnostic [CORBA][corba] interface onto the [ModeShape][modeshape] JCR implementation.


Speecifically, the _Source Tree as Workspace_ model - denoted in the previous - may be analyzed for purpose of _generalizing_ the model for re-use in a practical organization and management of _similar work_ - such as in construction of _commercial web sites_ utilizing _Java web components_, onto the _scalable, cloud-service oriented_ [Red Hat OpenShift][oso] platform, with its baseline operating system, Red Hat Enterprise Linux. The development of the `portal-gproj-manage` _source tree_ would bear some particular focus, on that note, as for that _source tree_ serving as an intermediary component between an _upstream web application archive_ and a developer-managed _web application server_.

Alternately, along perhaps a more expresseive _arc_, the _Source Tree as Workspace_ model may be considered for its applicability in development of _creative process support tools_, as may be developed onto an existing desktop application framework, namely the [Eclipse platform][eclipse], and as may be extended onto in development of mobile content development tools, such as may be applied typically in distributed workflows, towards a goal of some formal content development process though in a sense not, _per se_, _welded to an office network_.


### Disjunct Hosting for Static and Dynamic Online Content

The _static content web site_ component of the model was defined for use primarily in and while _bootstrapping_ the _dynamic content service_ components comprising the `portal-gproj`application, in its design and in its current iteration of development. Insofar as the _static content web site_ component providing a service for publishing a set of _static content resources_ such as [Maven][mvn] program _artifacts_ and [OWL][owl] _ontologies_ - the set of the latter, developed in the GProj _knowledge modeling_ work area - the _static site_ component in the model may serve a continued use, even after successful implementation of the _dynamic content service_ component, in the development of the _web presence_ of the _managing project_, namely the Gazebo Project.

The Gazebo Project represents a free/open source software development _work area_, as well as a set of _web resources_ corresponding to that _work area_, altogether as a non-commercial work in extension and development of free/open source software components, in development of essentially a transparent management process. Inasmuch, the development of the Gazebo Project's _web presence_ may entail development of such _web services_ as may be used in distribution of such _static content_ as the Gazebo Project may develop and inasmuch distribute, during the lifetime of the project. 

In the development of those _web services_ as such - with, so to speak, no requirement for any innovative refactoring of _the wheel_ as a design, in _this project_ - it may be deemed to be _pragmatically reasonable_ to serve the _static content_ directly via a conventional HTTP server, without any  _program platform components_ intervening between the _static content_ and its distribution via HTTP. So far as that the _distribution model_ for those components does not require any procedures for _user authentication_, _user authorization_, _user notification_, or _downloads monitoring_ - those components being licensed, typically, under terms of the [EPL][epl], and neither incorporating nor extending such software components as that such redistribution would entail limitation due to national and international software export/import guidelines, furthermore and lastly, being published as products of _technical application_, not as products of _marketing_ - _those components_ can be distributed directly as _static content_, for use within program systems such as may utilize, respectively, [Maven][mvn] and [Protege][protege]. 

GitHub in itself provides - namely, via the _[GitHub Pages][ghPages]_ feature, in addition to GitHub's broader support of the Git user base and GitHub's role as a public and private _Git repository service_ provider - GitHub provides such a _static web content provider service_ as may be used to publish those resources as _static resources_. Furthermore, the administrator and chief developer of the Gazebo Project trusts, personally, that GitHub shall provide such an online service, consistently, throughout the lifetime of the Gazebo Project.

In regards to one possible, alternate design for such a combined static/dynamic web content model: Frankly, an Nginx cartridge installed under OpenShift might be preferred as an altenative to the _[GitHub Pages][ghPages]_ provider, in regards to publication of low-demand, static content. However, in the _service design_ of the _portal-gproj_ application, the application is expected to make use of all three _small gears_ provided in a baseline OpenShift Online account, thus leaving no avilable gears for the Nginx installation, in the baseline model in which the project utilizes [OpenShift][oso] application services. So, alterntately, this project shall use the _[GitHub Pages][ghPages]_ feature, for publishing such static content as denoted in the previous. On a sidebar: Pending the development of anything resembling of the London Olympics _event news feed_ - cf. the ODC as affiliated with the International Olympic Committee - rather, for such low-volume traffic as expected for such static, shared resources as may be published within the GProj work area, the _[GitHub Pages][ghPages]_ feature may _suffice_.

### Mirroring the "IDE Workspace"

The [Eclipse IDE][eclipse], in its platform architecture, defines a _workspace_ model, such as is used within the [Eclipse IDE][eclipse]. Viewed as it being a graphical desktop application in a singular _user instance_, the [Eclipse IDE][eclipse] makes a _workspace_ model available to the user, in the [Eclipse IDE][eclipse]'s structured presentation of filesystem _folder_ and _file_ resources, and in presentation of further _project features_ as specified within a project's _file resources_ - as namely, presented in the _Project Navigator_ and _Package Navigator_ _view_ components, within the IDE. 

The Eclipse IDE workspace model defines, in its baseline, a model of "One workspace to zero or more projects and zero or more folder resources." Effectively, each _project_ in the _workspace_ may be _overlayed_ with features provided with zero or more _project facet_ instances, as provided intially by any one or more _plugins_ for the [Eclipse IDE][eclipse]. Pragmatically, in each _project_ organized within an Eclipse IDE _workspace_, the user may apply such procedural extensions and user interface overlays such as are published, _for instance_, by the [Eclipse Web Tools Platform][wtp] (WTP) and furthermore, the [Maven Integration for Eclipse][m2e]. 

[insert screenshots - illustrate workspace UI overlays as provided in UI presentation of projects having the WTP dynamic web module _facet_ and the M2E Maven _facet_ each _active_, in the Project Navigator view]

Essentially, the `gproj-web-workspace` project shall provide an Eclipse workspace for managing those source trees as denoted previously. The integration of the source trees and their dependency graphs, moreover, _shall be_ facilitated with the [Maven Integration for Eclipse][m2e], as from the point of _project import_ into the visual workspace presentation in an [Eclipse IDE][eclipse] instance, to each point of `mvn deploy:deploy` 

#### "Mirroring and Extending the IDE Workspace"

In a generic sense - as with regards to "the model illustated for its pragmatic applicability," in those components - the _workspace_ model may be extended for development of _addtional tooling_, not only in regards to the technical features of toolchains and procedures in _sofware development_, but furthermore for support of projects in  broader, essentially _creative_ domains - such as in technical designs, for design and publishing of electrical circuit designs onto the popular [Arduino] platform and its 32 bit alternative, the [Maple], as well as [Raspberry Pi], and in _creative_ projects such as may find support of software tools, components, and formal, known workflow procedures - as for supporting projects in domains such as computer raytracing, HTML5 and WebGL applications, and digital special effects design, as well as video, and more classical arts such as of music, performing arts, visual arts including photography, literary arts, also for broader project management, in a _multidisciplinary_ mode. Certainly, the [Eclipse IDE][eclipse] _workspace_ model can be _scaled_ to such extents.

(Ed. note: Though a _simple list_, as such, may seem  _eclectic_ in its focus, however perhaps it at least approaches an exhaustive definition of _creative fields_ such as are known to be supported and furthermore, extensibly suppotable of existing, free/open source software components. The propensity for free/open source software to be applied positively and progressively in supporting and contributing to development of original works in developmemt of cultural resources - as a topic - may be better off addressed in a mode of the _social sciences_, however - perhaps, in a manner _nonpartisan_ in all scientific principle, furthermore. Additionally, there's video game design, cf. Minecraft, by [Mojang][mojang] - and business models, those _institutional_ in corporate form and those _agile_ in so many non-monolithic approaches to _business practices_ and _business models_)


### Integration onto JCR

The primary design goal of the GProj Resource Lab is to define a CORBA model onto the ModeShape JCR implementation. (Ed. note: Abstractly, this design is developed in considerstion a design principle, stated, _"Do not reinvent the wheel, when the wheel does not need to be reinvented,"_ - it being a _software project_, not a _Mars rover design_, and not a _starship design_, _per se_.)


The GProj Resource Lab design will focus, technically, on three primary  project tasks:

* Define IDL for providing a comprehensive, platform-agnostic interface onto a standard JCR repository
* Define CORBA _object server_ implementations onto those IDL interface definitions, using ModeShape as the JCR _server_ component
* Define CORBA _object client_  implementations onto those IDL interface definitions, towards a broader goal of developing CORBA components for purpose of _creative workflow enablement_ and _business management process_

### Use Case: Developing the GProj Knowledge Model

Quoting the original _project summary_ published at the [gproj-portal web site][portal]:

> The Gazebo Project is a meta-project composed of a set of knowledge management projects and related work areas. The primary focus of the Gazebo Project is to develop a set of components and toolchains for tasks in knowledge management, in support of knowledge resource utilization and knowledge resource development, as centered around social concerns including:
>
> * Natural resource conservation
> * Recreational activity, with regards to national and continental geological and ecological heritage in the US and broader North America
> * Democratic access to information published for the collective audience of "We," the citizen stakeholders, published actively by US federal, state, county, and municipal governmental agencies
> * History of the arts, centering around the modern arts
> * Sports and recreation, in traditional modes reified of the international Olympics and in unconventional modes defined by commercial agencies including Red Bull GmbH and the Monster beverage company
> * The emerging NewSpace industry and the heritage of science and goodwill as codified in modes of traditional, institutional programs in aerospace systems development and space exploration
> * International humanitarian programs, such as managed by the UN and the ICRC

Each of those _points_ denotes a _work area_, centering around a _concept_ if not a formal [OWL][owl] _ontology_ as may be applicable towards developing a discrete _knowledge model_ and _knowledge resource management_ process, within a web portal context, for purposes of discrete _knwoledge sharing_ and effective _knowledge resource utilization_ in development of pragmatic, if not entrepreneurial works in those _concept domains_. In a sense, it may be an expression of _cultural intelligence_, without a _"big data"_ modality, focusing not on mere scraps of information, but rather on the human potential for _knowledge development_ as codified in _pure science_. (Ed note: If I could make _"One last pitch,"_ that would be _it._)


### Integration onto JCR and Git

In regards to the third of those project tasks, some specific focus should be made with regards to the roles of a JCR server in managing _versionable nodes_ in JCR -- cf. [JSR-283][jsr283], clause 15, _Versioning_. That focus may be made not only in considerstion of the baseline versioning model defined in JCR 2.0, but furthermore in considerstion of the _read-only_ Git _connector_ for ModeShape -- cf. [ModeShape Guide][modeshape-guide], subclause _[Git connector][modeshape-git-conn]_ -- and the [JGit][jgit] API -- as towards two ideal outcomes:

* _**"Upstream Git Synchronization"**_ -- Developing a methodology for read/write access onto a central Git repository, via JCR 2.0 -- essentially, in regarding a JCR _node graph_ as representing _the_ filesystem interacting with a remote JCR repository. In this task, [JGit][jgit] may be used as a sort of _pluggable SCCM proxy_ via JCR. (Ed. note: UML models may accompany this design goal. A "First goal," in that, may be to develop a set of UML models and accompanying BPMN diagrams, illustrating application of individual _Git commands_ in an abstract revision managememt process in Git. "Thus, towards platform agnosticism." This task may also be accompanied with extension of the JCR node types defined by the [ModeShape][modeshape] Git connector)

* _**"JCR like Git"**_ -- Developing a _"Git-like" interface_ onto JCR _full_ repository versioning, including full support for _branching_ and _merging_ within JCR _node graphs_ (cf. [JSR-283][jsr283], subclause 3.13.1.5, _"Simple and Full Versioning"_) This task may be accompanied with the development of [Eclipse IDE][eclipse] extensions, including an _[IResource][IResource]_ model onto JCR, a _Server Type_ for remote JCR connections, a _Team Provider_ onto JCR _versioning_ and such JCR node types as may be suitable for modeling of [Eclipse IDE][eclipse] _workspace_ and _project_ _metadata files_ and _metadata properties_

### Further Applications of ModeShape

(Sidebar: Note the Infinispan support inclided in ModeShape, "plus plus")

#### ModeShape OSGi Deployment

(probably some existing work, in this regards. "Look it up." Use case: towards using Eclipse platform components for developing a stand-alone, modular, in effect multidisciplinary desktop tool framework extensible onto distinct creative workflows, for creative workflow support, one _Resource Lab Desktop_. Note, furthermore, _ModeShape is not Eclipse Equinox_. The latter is the OSGi runtime developed in the Eclipse platform. The former is the JCR implementation around which GProj ResourceLab JCR extensions shall be developed, albeit ideally in as portable a manner as possible, cf.  Jackrabbit, Adobe _Day_. Also note, Apache Felix as an alternate OSGi framework.)

#### Developing a Project Management Model onto ModeShape

* Permissions model - (note the `jcr:versionManagement` _JCR privilege_. Note, also, PicketLink IDM, as used in GateIn. Kerberos integration for the Eclipse IDE and Eclipse IDE plugins?)

* Tools model: (Eclipse IDE? Resource Lab Desktop? Mobile integration, a _must_.)

#### WebDAV Contexts

(Alternately, **refer to: [ModeShape Sequencers, Built-In](https://docs.jboss.org/author/display/MODE/Built-in+sequencers)**)

**Use Case:** Using ModeShape to synchronize _file nodes_ with mobile thin clients, via the ModeShape _WebDAV service_, provide modular _hooks_ for WebDAV _presentation_, _import_, and _synchronization_ onto the underlying JCR _nodes_ model. (e.g transform the OmniFocus tasks bundle into/from a set of corresponding 'task' nodes; transform iThoughts mindmap into node graph, with links and pictures and so on; transform OmniGraffle diagram into ... SVG nodes?; GoodReader synch with PDF _document library_ context, "with bibtex support"; Textastic synch with project workspaces; something for OpenShift app monitoring support, perhaps, cf. Nagios; etc)

**Work Interface:** ModeShape WebDAV service, cf. _`modeshape-web-jcr-webdav-war-<version>.war`_ (as OSGi bundle?)

**Notes - Planning**

* Those _modular hooks_ may be provided such as to be _installed_ and _activated_ as _OSGi bundles_. (Question: What existing work may there be, planning included, with regards to OSGi _bundling_ of ModeShape? Note also, OSGi bundle distribution models, such as may be represented effectively in the _Eclipse Updates_ API and model. Sidebar - Mobile apps / thin client context: _OSGi and the Android platform?_)


#### GProj Resource Labs Testing Platform

**Platform Requirememts:**

* Must provide one or more JCR repositories via ModeShape
* Must provide the ModeShape WebDAV service
* May provide a Java web portal implementation, such as _[Jetspeed 2][jetspeed]_, for prototyping of browser-based interaction models onto underlying ModeShape services (_**Note:**_ This may entail a redesign of the `portal-gproj-manage` work area and the underlying _`portal`_ application, namely as for the purpose of developing a Jetspeed portal with the latter - as contrasted to the current design of the application, in which, [Liferay][liferay] has been proposed as the portal framework, in it providing a methodology for _rapid, web-based, web design prototyping_ and _web content management_, as a JSR-286 portal implementation, albeit perhaps in a manner more _resource intensive_ than JetSpeed, on the _server tier_. To furthermore develop a web content management framework integrating OWL ontologies and JCR, onto ModeShape, it may not be unwise to "Start from scratch," in extending the baseline _Java web portal_ framework, in this free/open source software project)
* Should incorporate features of a Java web application server, such as JBoss AS7 (Concern: Jetspeed on JBoss AS7? Altrnately, Glassfish on OpenShift, "DIY," might not scale. So, "To do," as a prereq to the web portal interface support, JetSpeed on JBoss AS7? Note also, [JetSpeed Deployment Guide](http://portals.apache.org/jetspeed-2/deployguide/), which denotes that JetSpeed makes extensive use of Spring components. "Then," there's OSGi....)
* Note: [ModeShape WebDAV Server, ModeShape Reference Manual 2.8.3](http://docs.jboss.org/modeshape/2.8.3.Final/manuals/reference/html/web_access.html#webdav_server)
* **See also:** _[ModeShape and JBoss AS7 and EAP](https://docs.jboss.org/author/display/MODE/ModeShape+and+JBoss+AS7+and+EAP)_, from the [ModeShape Guide][modeshape-guide] (onto newer ModeShape releases). The guide includes [a section on providing the ModeShape WebDAV service via JBoss EAP](https://docs.jboss.org/author/display/MODE/Using+Repositories+with+WebDAV+in+EAP)

## Endnote: "The Initial Comment"

The text of the comment from the [gproj-project-manage][gproj-project-manage] _README_ file, denoting the original _abstract workspace model_ as a design concept applicable onto [JCR 2.0][jsr283] and the [Eclipse IDE][eclipse] was as follows. The comment is retained here, for purpose of reference.

> From a _component modeling_ standpoint, this _alternate configuration_ introduces a _workspace model_ into the _SCCM information space_, as may resemble a _resource model_ in the _IDE information space_ - specifically, as with regards to a _workspace_ paradigm reified in the [Eclipse IDE](http://www.eclipse.org/). Furthermore, a _resource model_ of type _workspace_ is reified alternately, within the JCR content modeling framework, as in [JSR-283](https://jcp.org/en/jsr/detail?id=283). With regards to models for _distributed workspaces_ and _distributed development_, broadly, perhaps this abstract similarity of models _may bear some further consideration_, as towards practical concerns with regards to overall _content development tooling_ and innovations in _content management systems development_. 

[gproj-project-manage]: https://github.com/GazeboHub/gproj-project-manage
[oso]: https://www.openshift.com/
[mvn]: http://maven.apache.org/
[protege]: http://protege.stanford.edu/
[eclipse]: http://www.eclipse.org/
[jsr283]: https://jcp.org/en/jsr/detail?id=283
[modeshape]: http://www.jboss.org/modeshape
[modeshape-guide]: https://docs.jboss.org/author/display/MODE/ModeShape+Guide
[epl]: http://www.eclipse.org/legal/epl-v10.html
[wtp]: http://www.eclipse.org/webtools/
[m2e]: http://www.eclipse.org/m2e/
[m2e-wtp]: http://www.eclipse.org/m2e-wtp/
[liferay]: http://www.liferay.com/
[uml]: http://www.uml.org/
[sysml]: http://www.omgsysml.org/
[portal]: http://portal-gproj.rhcloud.com/
[ghPages]: http://pages.github.com/
[gproj-io]: http://gazebohub.github.io/
[jgit]: http://www.eclipse.org/jgit/
[modeshape-git-conn]: https://docs.jboss.org/author/display/MODE/Git+connector
[owl]: http://www.w3.org/2001/sw/wiki/OWL
[jbossas]: http://www.jboss.org/jbossas
[postgres]: http://www.postgresql.org/
[osonline]: https://www.openshift.com/products/online
[archetype-oo-servlet-manage]: https://github.com/GazeboHub/archetype-oso-servlet-manage
[mojang]: https://mojang.com/
[IResource]: http://wiki.eclipse.org/Resources
[jetspeed]: http://portals.apache.org/jetspeed-2
