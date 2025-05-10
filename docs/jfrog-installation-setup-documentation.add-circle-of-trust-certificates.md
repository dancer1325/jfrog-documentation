https://jfrog.com/help/r/jfrog-installation-setup-documentation/add-circle-of-trust-certificates

* steps
  * `kubectl create secret generic nameGivenToTheSecret --from-file=pathToCertificate`
    * create a secret / contains the root certificate
    * _Example:_ 
      ```
      kubectl create secret generic edge-root-crt --from-file=./edge-root.crt
      ```
  * add
    ```yaml, title=values.yaml
    artifactory:
      #circleOfTrustCertificatesSecret: nameGivenToTheSecret
      circleOfTrustCertificatesSecret: edge-root-crt
    ```
  * `helm upgrade --install artifactory jfrog/artifactory -f values.yaml`
 