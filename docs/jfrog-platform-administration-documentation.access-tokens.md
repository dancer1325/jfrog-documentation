https://jfrog.com/help/r/jfrog-platform-administration-documentation/access-tokens

* ways to manage
  * [REST APIs](http/artifactory%20REST%20APIs/access/accessTokens.http)
  * | JFrog Platform UI, User Management, Access Tokens
    * TODO: Where ❓

* if you want to create 
  * admin tokens -> you need admin privileges
  * access tokens / project-specific -> you need project admin privileges

* capabilities
  * Cross-instance authentication
    * == access tokens can be used for authentication |
      * instance or cluster | they were created
      * OTHER instances and clusters / are part of the SAME [circle of trust](#circle-of-trust-cross-instance-authentication)
  * User and non-user authentication
    * _Example of non-user:_ CI server jobs
  * Time-based access control
    * == access tokens' expiry period
    * allows
      * controlling the period of time | grant access
  * Flexible scope
    * == control the level of access
    * assign groups | tokens 
  * Pairing tokens
    * == manage connections BETWEEN DIFFERENT JFrog microservices

* properties
  * `Subject`
    * == user / -- associated to -- this access token 
      * ❌if it does NOT exist -> system will create a corresponding transient user❌
      * Administrators can -- assign a -- token | ANY subject (user)
      * NON-admin users / create tokens, can ONLY -- assign tokens to -- themselves
    * | create the access token, subject == username
    * | delete tokens, tokens of DIFFERENT users / SAME subject name -- will be -- deleted by design
  * `Scope`
    * == access token's scope
  * `Audience`
    * == set of instances or clusters | token -- may be -- identified by their [Service IDs](http/artifactory%20REST%20APIs/artifactSecurity.http)
      * Service ID == JFrog service or cluster's identifier
        * unique
        * internally generated
  * `Issuer`
    * == cluster's ID | access token was created
  * `Expiry`
    * == date & time | token will expire
    * recommendation
      * set [expirable tokens](#expirable-tokens)
  * `Issued at`
    * date & time | token was created
  * `ID`
    * == token ID

## created -- by -- project admins

* TODO:

## Expirable tokens

* expiry value
  * 👀as low as possible 👀
    * Reason: 🧠 reduce the risk of security vulnerabilities 🧠
  * \< persisted tokens' threshold 
    * Reason:🧠 
      * enhance performance
      * avoid UNNECESSARY checks | database🧠
* expiry period
  * long / complete the sequence of operations / token was created
    * Reason: 🧠OTHERWISE, | that sequence, it needs to be refreshed or recreated🧠

## Circle of Trust (Cross-Instance Authentication)

* requirements
  * access -- to the -- target Platform Deployments 
  * source Platform Deployments' root certificate
  * share a public certificate AMONG ALL participating instances

* cross-instance authentication -- through a -- "circle of trust"
  * -- supported by -- Access tokens
  * == 👀service verify access token signatures -- AGAINST -- ALL trusted certificates 👀
    * ALSO certificates / 
      * generated -- by -- OTHER services &
      * circle of trust == 'trusted' 
    * service administrator -- need to verify that -- ALL participating instances -- are equipped with the -- certificates
  * ANY instance -- can generate a -- token / used with any other instance within the circle of trust.

### use cases

* series of JPDs / need to be -- , via 1! set of credentials, -- accessed
  * _Example:_ 1! build agent / needs to
    * upload
    * download -- from -- 2 JPD instances
  * if you create a circle of trust -> ensure that 1 JPD instance -- will trust -- ANOTHER instance’s tokens
    * share the public token certificate BETWEEN ALL circle's instances

![](static/access-tokens1.png)

* \| run the sever (WITHOUT restarting), trusted certificates -- can be -- 
  * loaded
  * removed

### how to establish?

* TODO: