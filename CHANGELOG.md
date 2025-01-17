# Changelog

## 4.0.1+16.2.0

- fix yamllint issues (remove blank lines in CRD files)
- add `.yamllint`

## 4.0.0+16.2.0

- update Helm chart to `v16.2.0`
- use Traefik `v2.9.4`

## 3.1.1+10.24.4

- fix yamllint issues (remove blank lines in CRD files)

## 3.1.0+10.24.4

- update Helm chart to `v10.24.4`
- use Traefik `v2.8.7`
- add Github release action to push new release to Ansible Galaxy

## 3.0.0+10.24.2

- update Helm chart to `v10.24.2`
- use Traefik `v2.8.4`
- introduce `traefik_delegate_to` variable. Previously this was hard coded to `127.0.0.1` and it's also the default of this variable.
- introduce `traefik_helm_show_commands` variable (see README for more information)
- introduce `traefik_template_output_directory` variable (see README for more information)
- introduce `Molecule` tests
- don't use `shell` module anymore to execute `helm` command. Now `kubernetes.core.helm*` modules are used.
- use two underscores for internal variables
- ansible-lint: fix various issues like using FQDN Ansible module names now
- add `requirements.yml`
- add `collections.yml`

## 2.8.3+10.24.1

- update Helm chart to `v10.24.1`
- use Traefik `v2.8.3`
- update Traefik CRDs to v2.8.x

## 2.6.6+10.19.5

- update Helm chart to `v10.19.5`
- use Traefik `v2.6.6`
- introduce `traefik_install_crds` variable (see README for more information)

## 2.3.0+10.14.1

- update Helm chart to `v10.14.1`
- use Traefik `v2.6.1`

**Important note:**: Make sure that the `middlewarestcp` CRD is updated before you upgrade e.g. via `curl https://raw.githubusercontent.com/traefik/traefik-helm-chart/v10.14.1/traefik/crds/middlewarestcp.yaml | kubectl apply -f -`

## 2.2.0+10.9.1

- update Helm chart to `v10.9.1`
- use Traefik `v2.5.6`
- fix linting issues
- remove unneeded directories

## 2.1.1+10.3.2

- update Helm chart to `v10.3.2`
- use Traefik `v2.5.2`

## 2.1.0+10.3.0

- update Helm chart to `v10.3.0`
- use Traefik `v2.5.0`

The following note is only relevant if you upgrade from a chart version `< v10.3.0` (which introduced Traefik `v2.5.0`). For new installations it's not relevant.

**Important note:** Before upgrading read this issue [](https://github.com/traefik/traefik-helm-chart/issues/359) as it may hit you if you upgrade from a chart version `< v10.3.0` (which introduced Traefik `v2.5.0`). If you already have a `CustomResourceDefinition` (CRD) called `middlewaretcps.traefik.containo.us` (check with `kubectl describe crds middlewaretcps.traefik.containo.us`) upgrade shouldn't be an issue.

You've basically two options:

- make sure that the CRD is installed before you upgrade e.g. via `curl https://raw.githubusercontent.com/traefik/traefik-helm-chart/master/traefik/crds/middlewarestcp.yaml | kubectl apply -f -`
- delete the Traefik resources via `ansible-playbook --tags=role-traefik-kubernetes --extra-vars action=delete k8s.yml` and install again via `ansible-playbook --tags=role-traefik-kubernetes --extra-vars action=install k8s.yml`. This also adds the new CRD `middlewaretcps.traefik.containo.us`. This of course will uninstall Traefik! So all ingress traffic will be offline until you install Traefik again.

## 2.0.1+10.1.1

- update README

## 2.0.0+10.1.1

- update Helm chart to `v10.1.1`
- Traefik Helm chart version >= `v10.x.x` needs at least Kubernetes `v1.16`
- use Traefik `v2.4.13`
- Default Traefik version is now specified in `templates/traefik_values_default.yml.j2`

## 1.1.0+9.19.1

- update Helm chart to `v9.19.1` (uses Traefik `v2.4.8`)

**Important note:** Before upgrading read this issue [](https://github.com/traefik/traefik-helm-chart/issues/359) as it may hit you if you upgrade from a chart version `< v9.13.0` (which introduced Traefik `v2.4.0`). If you already have a `CustomResourceDefinition` (CRD) called `serverstransports.traefik.containo.us` (check with `kubectl get crds serverstransports.traefik.containo.us`) upgrade shouldn't be an issue.

You've basically two options:

- make sure that the CRD is installed before you upgrade e.g. via `curl https://raw.githubusercontent.com/traefik/traefik-helm-chart/master/traefik/crds/serverstransports.yaml | kubectl apply -f -`
- delete the Traefik resources via `ansible-playbook --tags=role-traefik-kubernetes --extra-vars action=delete k8s.yml` and install again via `ansible-playbook --tags=role-traefik-kubernetes --extra-vars action=install k8s.yml`. This also adds the new CRD `serverstransports.traefik.containo.us`. This of course will uninstall Traefik! So all ingress traffic will be offline until you install Traefik again.

## 1.0.0+9.12.3

- initial commit for Traefik `v2.3.6`
