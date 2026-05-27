# OpenAPI Learn

Source: https://learn.openapis.org/

- 
- 
- 
- Getting Started 
- 
- Fork me on GitHub Skip to main content Menu Expand (external link) 
- Document Search Copy Copied 
- Getting Started 
- Introduction 
- Glossary 
- The OpenAPI Specification Explained 
- Structure of an OpenAPI Description 
- API Endpoints 
- HTTP Methods 
- Content of Message Bodies 
- Parameters and Payload of an Operation 
- Reusing Description 
- Providing Documentation and Examples 
- API Servers 
- Describing API Security 
- Enhanced Tags 
- Providing Callbacks 
- Providing Webhooks 
- Implementing Links 
- Sequential Media Types 
- Best Practices 
- Upgrading Between Versions 
- Overlay - Upgrading Between Versions 1.0 and 1.1 
- Upgrading from OpenAPI 3.0 to 3.1 
- Upgrading from OpenAPI 3.1 to 3.2 
- Using References 
- References Overview 
- Resolve References 
- Remove References 
- Dynamic References 
- Example API Descriptions 
- 3.2-query-example 
- 3.2-tags-example 
- api-with-examples 
- callback-example 
- link-example 
- non-oauth-scopes 
- petstore 
- petstore-expanded 
- tictactoe 
- uspto 
- webhook-example 
- Overlays 
- Example: add a license 
- Example: tag DELETE operations 
- Example: add params selectively 
- Example: copy a schema 
- Community This site uses Just the Docs , a documentation theme for Jekyll. Search OpenAPI Documentation 
# Getting started 
 
## Intended Audience 
 This guide is directed at HTTP-based API designers and writers wishing to benefit from having their API formalized in an OpenAPI Description ( OAD ).

 Machine-readable API descriptions are ubiquitous nowadays and OpenAPI is the most broadly adopted industry standard for describing new APIs . It is therefore worth learning it and getting it right from the start.

 These pages are a companion to the OpenAPI Specification (OAS), helping the reader learn it and answering questions like “What is the best way to accomplish… ?” or “What is the purpose of… ?” that are naturally out of the scope of the specification.

 
- If you are unsure if this guide is for you, read the next section below. 
- If you do not know what “API”, “machine-readable description” or “OpenAPI” mean start by reading the Introduction chapter. 
- If this is your first time writing an OpenAPI Description read The OpenAPI Specification explained chapter for step-by-step tutorials. 
- If you already have OpenAPI experience but need help with a specific topic, take a look at the index of The OpenAPI Specification explained chapter; it also includes advanced topics. 
- Finally, make sure you are aware of the recommended Best Practices to take full advantage of OpenAPI ! 
- And of course, you can always refer to the actual OpenAPI Specification for reference. 
## Advantages of Using OpenAPI 
 Having your API formally described in a machine-readable format allows automated tools to process it, instantly opening the door to:

 
- Description Validation and Linting : Check that your description file is syntactically correct and adheres to a specific version of the Specification and the rest of your team’s formatting guidelines. 
- Data Validation : Check that the data flowing through your API (in both directions) is correct, during development and once deployed. 
- Documentation Generation : Create traditional human-readable documentation based on the machine-readable description, which always stays up-to-date. 
- Code Generation : Create both server and client code in any programming language, freeing developers from having to perform data validation or write SDK glue code, for example. 
- Graphical Editors : Allow easy creation of description files using a GUI instead of typing them by hand. 
- Mock Servers : Create fake servers providing example responses that you and your customers can start testing with before you write a single line of code. 
- Security Analysis : Discover possible vulnerabilities at the API design stage instead of much, much later. On top of this, the OpenAPI Specification also provides you with:

 
- A non-proprietary format : You have a say in the future direction of the Specification! 
- The most developed tooling ecosystem : As a direct result of the previous statement, OpenAPI offers a vast number of tools to work with it. Just take a quick look at OpenAPI Tooling . 
- A format readable by both machines and humans : Even though writing OADs by hand is not the most convenient way of doing it (See Best Practices ), they are plain text files which can be easily browsed in case something needs to be debugged. So, choose your desired entry point from the list at the top of this page and start your journey!

 © 2025 OpenAPI Initiative. 
This work is licensed under a Creative Commons Attribution 4.0 International License . The documentation is maintained in https://github.com/OAI/learn.openapis.org/ .

 This site uses Just the Docs , a documentation theme for Jekyll.
