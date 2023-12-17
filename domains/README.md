# Feature Domains

A feature domain represents a domain that can implement a specific feature in your application.

| Feature Domain | Description |
|:---|:---|
|[`InMemoryCache`](#InMemoryCache-heading)|An in-memory cache is one that stays in RAM while a the microservice instance is running but is not persistent and must re-populate after the microservice is shut down and restarted. The cache is used only to cache objects of an entity by its unique ID.|
|[`AdminUI`](#AdminUI-heading)|This domain allows you to customize how an admin console is constructed based on your entity model.|
|[`Security`](#Security-heading)|This domain is concerned about the security and user administration features in the application.|
|[`DocumentBuilder`](#DocumentBuilder-heading)|This domain allows one to customize how code is generated that will take entity attribute values and build a document with them.|
|[`Localization`](#Localization-heading)|The Localization domain is used for configurating code generation related to localization.|

Each of the feature domains are explained in more detail in their own section below.

<a name="InMemoryCache-heading"></a>
## InMemoryCache

An in-memory cache is one that stays in RAM while a the microservice instance is running but is not persistent and must re-populate after the microservice is shut down and restarted. The cache is used only to cache objects of an entity by its unique ID. The tags provide a way to customize the cache.

### Entity Tags

These tags can be placed on an entity itself.

| Tag | Description |
|:---|:---|
|`enable`|Enables a cache on an entity.|
|`size`|Allows the specification of a cache size.|
|`type`|Allows the specification of the type of cache.|



<a name="AdminUI-heading"></a>
## AdminUI

This domain allows you to customize how an admin console is constructed based on your entity model. The customization is done by applying the tags described here on the entities, attributes and relationships in your model.

The admin console is comprised of basically three typs of web pages, each described below.

### Admin Home Page

This is the top most page of the admin console. It can be configured to include summary views of the top level entities. From each object of an entity you can go to the detail page. To have an entity show up on this page, simply tag it with `home`. To also make it so the admin can create new objects of a home page entity, tag it with `edit`.

### Admin Detail Page

Whenever you click on a link of an object it takes to this detail page. This will let an admin see and edit the object for the attributes that you choose, just tag them with `detail`.

Markdown for string attributes is also supported. Simply tag an attribute with `markdown` and when editing, the admin will be given a web-based markdown editor. As well, it will be rendered to HTML for viewing.

This page can also build a table for `many` relationships, just tag them with `detail`. This table is considered a "summary" view of the entity on the other side of this relationship. The columns of the table are attributes of the relationship entity and you can control which are visible in this summary table by tagging those attributes with the `summary` tag.

At the top of the admin detail page there are two configurable elements: a **breadcrumb bar** and a **headline**.

#### Breadcrumb bar

A breadcrumb bar generally tells the user where they are in some kind of hierarchy or view history. In our case it represents the hierarchy of your model, starting with the `home` entities on the admin home page then cascades as the admin clicks on the relationships shown in a detail page. Each item in the breadcrumb list is represented by an entity and you can customize how an entity's item will look using tags. A breadcrumb item can have three components:

*prefix* *number*: *title*

The *prefix* can be the entity's name, just tag the entity with `breadcrumb:prefix`. The *number* can be from an integer attribute of the entity, just tag it with `breadcrumb:number`. Finally the *title* can be from a string attribute of the entity, just tag it with `breadcrumb:title`. Examples are: "Module 1: Introduction" (has all three components), "Step 4" (only has the *prefix* and *number*).

#### Headline

The headline lets the admin know what they are looking at without having to look at the individual attributes. You construct the headline from attributes of the entity or the entity name itself. Like a breadcrumb item, a headline can have three components:

*prefix* *number*: *title*

The *prefix* can be the entity's name, just tag the entity with `headline:prefix`. The *number* can be from an integer attribute of the entity, just tag it with `headline:number`. Finally the *title* can be from a string attribute of the entity, just tag it with `headline:title`. Examples are: "Module 1: Introduction" (has all three components), "Step 4" (only has the *prefix* and *number*).

### Admin New Object Page

When the admin clicks on a "New ..." button, they will be taken to this page. There are no available customization tags for this page.



### Entity Tags

These tags can be placed on an entity itself.

| Tag | Description |
|:---|:---|
|`breadcrumb:prefix`|The breadcrumb bar is part of the detail page for an entity and it helps navigate the hierarchy of your admin console. Placing this tag on an entity means that the entity name will be used in the breadcrumb item for this entity.|
|`edit`|When an entity is tagged with this tag the admin console home page will provide a button to allow you create new objects of this entity.|
|`headline:prefix`|The headline is part of the detail page for an entity. Placing this tag on an entity means that the entity name will be part of the header part of this headline.|
|`home`|Placing this tag on an entity designates it to be included on the home page of the admin console.|
|`paging:size`|When an admin "home" page is created for an entity, the value assigned to this tag is used as the number of items per page to show. As well, pagination UI is included so the user can advance or go back pages.|

### Attribute Tags

These tags can be placed on the attribute of an entity.

| Tag | Description |
|:---|:---|
|`breadcrumb:number`|Tagging an integer attribute with this tag will include it in the breadcrumb bar item as the number.|
|`breadcrumb:title`|Tagging a string attribute with this tag will include it in the breadcrumb bar item as the title.|
|`detail`|Tagging an attribute with this tag will ensure that it will be included on the admin console detail page for the corresponding entity.|
|`headline:number`|Tagging an integer attribute with this tag will include it in the headline as the number.|
|`headline:title`|Tagging a string attribute with this tag will include it in the headline as the title.|
|`markdown`|If the text of a string attribute is markdown text, then tagging that attribute with this tag will both allow it to be rendered to HTML for display and also when the admin edits the attribute, a web-based markdown editor will be used.|
|`summary`|Tagging an attribute with this tag will allow it to be included in a summary view of its entity.|

### Relationship Tags

These tags can be placed on the relationships of an entity.

| Tag | Description |
|:---|:---|
|`detail`|Tagging a relationship with this tag will ensure that it will be included on the admin console detail page for the corresponding entity.|
|`display:attribute`|When displaying a selected to-one relationship object, this tag should be assigned to the name of the attribute of the selected object that should be used.|
|`filter:attribute`|When tagging a relationship with this tag, you are requesting to filter based on a particular attribute value of the objects on the other side of the relationship. **Currently only attributes of type enum are supported. The attribute value is specified with a tag of `filter:value` When the admin panel lets you edit this relationship, it will present you with some kind of pulldown list - and it will be filtered based on the value you specified.|
|`filter:value`|This is used in conjunction with `filter:attribute` to provide a value to filter by. For instance, if you want to filter by an enum item of say `EARTH` on an attribute named `planet` you would have two tags: `T "filter:attribute" = "planet", "filter:value" = "EARTH"`.|

<a name="Security-heading"></a>
## Security

This domain is concerned about the security and user administration features in the application.

### Authentication (Login)

Applications that have user specific data (that is, require users to register and have an account) define some type of "user" entity. This entity also usually has an attribute for storing their username (whether it be an email address or a simple string) and an attribute for storing an encoded password.

To denote which entity represents your "user" entity, simply tag it with `user`. Inside this entity the attribute to be used for their username should be tagged with `login:username` and the attribute to be used to store their encoded password should be tagged with `login:password`. If the username attribute is also an email address, you can tag it with `email` and it will be treated as such.

### Authorization (Roles)

Roles are a way to group users for the purpose of controlling access to resources on the server. There is usually specific code that controls how each role has access to specific resources. This domain provides tags that let you configure not just the roles but how the roles enforce specific types of access.

Lets start with defining the roles. There needs to be an `enum` that has an item for each role you want to use to control access. This enum must be used in the `user` tagged entity as a `many` attribute (meaning a user can be assigned multiple roles). First tag the enum with `role` then tag each item of the enum with a tag that starts with `role:` followed by the name of the role (e.g., `role:admin`). You will then use these item tags when constructing tags applied to entites that you want to control access to.

There are two supported access types: read and write. Read access is for GET endpoints and write is for POST, PUT and DELETE endpoints. To set write access for an entity, tag the entity with a tag that starts with `access:write:` and ends with your role tag (e.g., `access:write:role:admin`). This will make sure only users with that role can perform write actions on objects of that entity. The same can be done for read access as well. If you don't tag an entity with an access type, it will imply that any authenticated user can perform that operation.

### User Administration





### Entity Tags

These tags can be placed on an entity itself.

| Tag | Description |
|:---|:---|
|`access:delete:`|An entity that has a tag that starts with this indicates it is trying to assign a role that has delete access. The remaining part of the tag represents the role. If you also tag an enum item of the designated "role" enum with this tag, it will assign that role to have delete access. If no role is assigned for delete access, write access role(s) will be used.|
|`access:object:level`|When an entity is tagged with this tag, it means that you want to enable the ability to control user level access unique for each object of this entity.|
|`access:read:`|An entity that has a tag that starts with this indicates it is trying to assign a role that has read access. The remaining part of the tag represents the role. If you also tag an enum item of the designated "role" enum with this tag, it will assign that role to have read access.|
|`access:write:`|An entity that has a tag that starts with this indicates it is trying to assign a role that has write access. The remaining part of the tag represents the role. If you also tag an enum item of the designated "role" enum with this tag, it will assign that role to have write access.|
|`user`|An entity tagged with this indicates that it represents a logged in user. You entire entity model should have only one entity tagged with this. It is used during code generation to know where user specific data is stored.|

### Attribute Tags

These tags can be placed on the attribute of an entity.

| Tag | Description |
|:---|:---|
|`email`|This tag should be placed on an attribute of the entity tagged with "user" that represents the user's email address.|
|`login:enabled`|This tag should be placed on an attribute of the entity tagged with "user" that indicates if the user account is enabled.|
|`login:password`|This tag should be placed on an attribute of the entity tagged with "user" that represents the user's password (encoded or not).|
|`login:username`|This tag should be placed on an attribute of the entity tagged with "user" that represents the user's username (which could also be their email).|
|`name:first`|This tag should be placed on an attribute of the entity tagged with "user" that represents the user's first name.|
|`name:last`|This tag should be placed on an attribute of the entity tagged with "user" that represents the user's last name.|


<a name="DocumentBuilder-heading"></a>
## DocumentBuilder

This domain allows one to customize how code is generated that will take entity attribute values and build a document with them.

The type of document that can be created will have some hierarchy where it has sections and subsections. You have some control of how section titles are constructed as well. It works best when its used to render a document format such as markdown that has the required formatting elements.

If we look at a typical structured document we have sections that have a header portion and a body. You can have sections inside other sections to create hierarchy. This creation of hierarchy is also supported where a specific entity would represent a specific level in the document and its "child" entities (those it has a relationship with) can be used to create sub-sections.

A section heading for an entity can be constructed from elements of the entity. The section heading has three parts:

*prefix* *number*: *title*

The *prefix* can come from only the entity name and will be a title-ized version of the entity name. Just tag the entity with `section:prefix` to have it included in the heading. The *number* can come from an integer attribute of entity, just tag the attribute with `section:number`. If either a prefix or number is specified, it will be followed by a colon `:` character. The *title* can come from a string attribute, just tag it with `section:title`. All three elements are **optional**. Example headings are: "Module 1: Introduction" (all three elements), "Summary" (only title), "Step 5" (prefix and number only).



### Entity Tags

These tags can be placed on an entity itself.

| Tag | Description |
|:---|:---|
|`section:prefix`|Tagging an entity with this tag indicates that the name of the entity should be used in any section header of the document that is constructed for this entity.|
|`top`|This should be placed on any entity that represents the top of a document. By tagging an entity with this tag you are essentially saying you want code that will generate a document where this entity defines the top content of the document.|

### Attribute Tags

These tags can be placed on the attribute of an entity.

| Tag | Description |
|:---|:---|
|`if:multiple`|This is used in conjunction with the `section:number` tag to indicate that it should only include the number if the total number of such sections will be greater than 1.|
|`section:body`|The string attribute that is to supply the body of the section should be tagged with this tag.|
|`section:number`|This should be used on an integer attribute that provides a number in a sequence that is relavent for objects of this entity in a particular scope. For instance if the entity was Step, this could be used to construct section headings Step 1, Step 2, etc.|
|`section:title`|This is applied to any string attribute that is to be used as a title text for a section header.|
|`subsection`|Tagging a string attribute with this tag causes its text to be included as a sub-section (after the section body) where its sub-section header is taken from the attribute name. If you want the sub-section header to be different than the attribute name, simply rename the attribute in this domain. If you don't want a sub-section header, simply additionally add the tag `untitled`.|
|`untitled`|This is used in conjunction with the `subsection` tag to indicate that you don't want the sub-section to have a heading.|

### Relationship Tags

These tags can be placed on the relationships of an entity.

| Tag | Description |
|:---|:---|
|`subsection`|Tagging a relationship with this tag indicates you want to create a sub-section for each object that exists in that relationship. The formatting for its section header is defined by that entity. This is how you can create hierarchy in the document.|

<a name="Localization-heading"></a>
## Localization

The Localization domain is used for configurating code generation related to localization.

Localization of application text is often handled/supported by the particular application framework being used. This feature domain is not concerned just about that but mostly about adding code to your application so that the dynamic content of application can be stored in multiple languages (localized). In order to do this it will require that you define specific entities and attributes that are tagged in such a way that supporting code can be generated.

### Discussion

Normally text can be stored in a simple `string` attribute. Of course, text in only one language can be stored this way. To expand this to multiple languages you essentially need three other entities:

- An entity that represents human languages. This should be tagged with `language`.

- An entity that represents the translation of the content in a specific language. This will contain the the actual localized text. The entity should be tagged with `content:localized` and the attribute of this entity that contains the localized text should be tagged as `content:text`. This entity should also have a `one` relationship with the `language` entity.

- An entity that represents the text you want to localize as **content**. The original text attribute is then replaced by a relationship to this content entity. This will allow it to be expanded to multiple languages. This entity should be tagged with `content` and have a `many` relationship with the `content:localized` entity.

If an application is going to adopt such a localization system then its very likely it will also need to support showing content in a user's preferred language. That is, it would be nice if there were methods available that would automatically resolve some content to a language that the user has designated as their preferred language. To support this, the entity that represents users of the system should be tagged with `user` and should have a relationship with the `language` entity that is tagged with `language:preferred`. Also, for each content field (relationship) that we want to have this ability, we need to define a `virtual string` attribute that is tagged with `content` that assigned a tag value of the name of the relationship that corresponds to the content. For instance if you have a relationship named `summaryContent` then the `virtual string` attribute tag would be `"content" = "summaryContent"`. This will ensure code is generated for that `virtual string` attribute to automatically supply the preferred language localization for the logged in user.

### Reference

For reference, the tags for this feature domain are described below:

### Entity Tags

These tags can be placed on an entity itself.

| Tag | Description |
|:---|:---|
|`content`|An entity that represents content as not language specific but just the content itself should be tagged with this tag. This entity should have a one-to-many relationship with an entity that keeps track of the content in a language specific way.|
|`content:localized`|An entity that represents language specific content should be tagged with this tag. This entity should have as its parent entity an entity tagged with `content`. Also, the entity should have a relationship with an entity tagged with `human:language`. Essentially this entity provides the localized content for all supported languages for all content.|
|`language`|Indicates that the entity keeps track of human languages. This will be used by the localization feature to keep track of the user's preferred language and also to keep track of language specific text.|

### Attribute Tags

These tags can be placed on the attribute of an entity.

| Tag | Description |
|:---|:---|
|`content`|When applying the tag `content` to a virtual attribute it denotes that it is part of a localization pattern whereby the value of the tag is the name of a relationship of the same entity and that relationship is to an entity tagged with a `content` tag. Code for this virtual attribute will be synthesized such that it has the content's text in the user's preferred language.|
|`content:text`|This should be used to tag an attribute in the entity tagged with `content:localized` that represents the actual localized text. The language of this text should be that of the `language` tagged entity associated with the parent entity of this attribute.|
|`language:code`|This should be used to tag the attribute of an entity tagged with `language` and represents an attribute that contains the ISO 639‑1 code of a language.|

### Relationship Tags

These tags can be placed on the relationships of an entity.

| Tag | Description |
|:---|:---|
|`language:preferred`|This tag is used to indicate the relationship of the user entity that represents the preferred language of the user. It must be placed on a relationship belonging to an entity tagged with `user` and the relationship must be to an entity that is tagged with `language`.|


# Base Domains

These are domains that provide the foundation for this library.

| Domain | Description |
|:---|:---|
|`APIPath`|How URL paths are constructed in the API is controlled by this domain.|
|`Asset`|This domain defines tags that allow you to customize how asset related entities are treated.|
|`Controller`|This domain is used for the generation of code that implements the first layer of the application's endpoints.|
|`Converter`|Converting Java objects to JSON is pretty straight forward, however for Protobuf it is more involved so this domain is used to control the generation of classes that perform the mapping of Java objects to protobuf data.|
|`DTO`|The Data Transfer Object domain controls how entities are represented between the server and the client.|
|`DTOMapper`|The generation of classes involved in mapping model object into dto objects is controlled by this domain.|
|`Database`|The SQL that represents the database for this microservice is controlled by this domain.|
|`Exception`|This domain provides a namespace for exception classes.|
|`JSONDTO`|This domain controls how the classes used for JSON based formatting will be generated.|
|`Model`|Data is moved to and from the database with Java objects. This domain controls how these Java classes are generated.|
|`Protobuf`|The classes created for this domain are responsible for how the protocol file is created.|
|`ProtobufDTO`|The Game is written to use Protobuf as the format medium of data. This domain controls how classes used for Protobuf based formatting will be generated.|
|`ReleasedJSONDTO`|This domain is specific for creating JSON DTO classes that represent released versioned objects.|
|`ReleasedModel`|Data is moved to and from the database with Java objects. This domain controls how these Java classes are generated.|
|`Repository`|The classes generated for this domain are responsible for moving data to and from the database.|
|`Service`|The classes generated for this domain provide the business logic for the application.|
|`StaticLocalization`|Static Localization refers to localized text that is part of the application itself and is **not** part of the user content.|
|`Utils`|The Utils domain is simply used for a namespace (provided by the specializer) to install utility classes.|
|`WebUserUI`|This domain is associated with web UI code that serves the "user" side of a web site (vs the admin side).|
