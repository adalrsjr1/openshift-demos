## Running applications

The Dockerfile must exposes a `<port>` to Openshift automagically create a service

1. Create application:

`oc new-app <https://github.com/...> --context-dir <folder of app in git directory> --strategy=docker -n <project-name> --name <application-name> -l name=<application-name>`

2. Track the build log:

`oc logs -f bc/<application-name>`

3. Expose route to service:

`oc expose svc/<application-name>`

4. Access the application:

`minishift openshift service <application-name> --in-browser`

## Scaling and RoundRobin

1. To scale:

`oc scale dc <deployment-name> --replicas=<n>`

2. Edit route configuration to use RoundRobin strategy:

`oc edit rount <deployment-name>`

  1. In edit file replace metadata/annotations with:
  ```
  metadata:
      annotations:
          haproxy.router.openshift.io/balance: roundrobin
          haproxy.router.openshift.io/disable_cookies: "true"
  ```
