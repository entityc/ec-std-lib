[//]: # ( =====preserve===== start-Introduction ===== )
# Document

The following templates are used to create documentation.

[//]: # ( =====preserve===== end-Introduction ===== )

> This document was created by template: `TemplateMarkdown`

<a name="template-summary"></a>
## Template Summary

|Template|Description|
|---|---|
| [`Confluence`](#confluence) | This template generates documentation in Confluence format of the modules, entities and attributes of a particular space. |
| [`DomainDocs`](#domain-docs) | This template will specifically document the domains in a space. Understanding the domains is important for template developers and architects developing a new application. |
| [`Markdown`](#markdown) | This template generates documentation in Markdown format of the modules, entities and attributes of a particular space. |
| [`TemplateMarkdown`](#template-markdown) | This template creates documentation for templates in markdown format. It does this for an entire directory tree. |

Each of the template files will be covered in more detail below.

<a name="confluence"></a>
## Confluence

This template generates documentation in Confluence format of the modules, entities and attributes of a particular space.

| |References|
|---|---|
| **Tags** |`asset:collection` `asset:file` |
| **Domains** |`Model` `DTO` |

### Functions

#### Asset Section

```
assetSection(attribute, collectionAttribute)
```

##### Inputs

|Name|Description|
|---|---|
|`attribute`||
|`collectionAttribute`||



<a name="domain-docs"></a>
## Domain Docs

This template will specifically document the domains in a space. Understanding the domains is important for template developers and architects developing a new application.

| |References|
|---|---|
| **Tags** |`feature` |

### Functions

#### Document Domain

```
documentDomain(domain)
```

Generates documentation for a specified domain.

##### Inputs

|Name|Description|
|---|---|
|`domain`|The domain to document.|



<a name="markdown"></a>
## Markdown

This template generates documentation in Markdown format of the modules, entities and attributes of a particular space.

| |References|
|---|---|
| **Domains** |`Model` `DTO` |

<a name="template-markdown"></a>
## Template Markdown

This template creates documentation for templates in markdown format. It does this for an entire directory tree. At each directory level it looks for template files and if any are found it generates a `README.md` file documenting all the templates of the directory.

### Functions

#### Document Author

```
documentAuthor(author)
```

Given a reference to an author, this will extract information such as the authoring to outlets.

##### Inputs

|Name|Description|
|---|---|
|`author`|The author to document.|



#### Document Publisher

```
documentPublisher(publisher)
```

Given a reference to a publisher, this will extract information such as its outlets.

##### Inputs

|Name|Description|
|---|---|
|`publisher`|The publisher to document.|



#### Document Template

```
documentTemplate(template, rootDirectory, directory)
```

Given a reference to a template, this will extract information such as its functions, descriptions like this, etc. and build a markdown document of the template.

##### Inputs

|Name|Description|
|---|---|
|`template`|The template to document.|
|`rootDirectory`|The top most directory of the documentation tree.|
|`directory`||



#### Document Directory

```
documentDirectory(configuration, rootDirectory, directory, recursive)
```

Looks in a specified directory and if there are any templates there it creates a README file that documents those templates.

##### Inputs

|Name|Description|
|---|---|
|`configuration`|Configuration in use.|
|`rootDirectory`|The top most directory of the documentation tree.|
|`directory`|The directory|
|`recursive`|If true it then recursively does this for sub directories.|



#### Document Function

```
documentFunction(fun)
```

Given a reference to a function, this will extract information such calls to other functions, descriptions like this, etc. and build a markdown document of the function.

##### Inputs

|Name|Description|
|---|---|
|`fun`|The function to document.|



