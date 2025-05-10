https://jfrog.com/help/r/jfrog-platform-administration-documentation/establish-the-circle-of-trust

* if the source is [trusted by the target Platform Deployment](jfrog-platform-administration-documentation.access-tokens.md) -> ONLY configure the synchronization of security entities

* | BEFORE proceeding to configure your Access Federation topologies, 
  * ⚠️guarantee EXIST REQUIRED root certificates | source access service⚠️
    ```
    $JFROG_HOME/artifactory/var/etc/access/keys/trusted 
    # folder
    ```

* if you want to establish circle of trust | Helm installation -> [here](jfrog-installation-setup-documentation.add-circle-of-trust-certificates.md)