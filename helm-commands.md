Bitnami and artifacthub are the repository for helm charts

# List helm repository
helm repo list

# Add Helm Repository
helm repo add name helmRepoUrl

# Search within the repository
helm search repo keywordname

# Update helm repo
helm repo update

# helm install
helm install releaseName repoName/chartName --> install the latest version
helm install releaseName repoName/chartName --version "x.x.x"

# helm list
helm list -n namespace
helm list --output=yaml

# uninstall helm
helm uninstall releaseName

# Helm Upgrade
helm upgrade releaseName repoName/chartName --set "image.tag=2.0"

# Helm List
helm list --deployed
helm list --uninstalled --> works only when the --keep-history flag is used
helm list --superseeded --> previous version

Chart.yaml contains name, appVersion,type of chart

Library Chart : utility chart
Application Chart

If tag is not provided in the values.yaml it will take the appVersion from the chart.yaml

# Print historical revisions for a release
helm history releaseName

# Status of the helm charts
helm status releaseName
helm status releaseName --show-resources

# Helm Rollback to previous version
helm rollback releaseName

# Removes all the associated resources and marks the release as deleted
# Also retains the release history which helps to rollback to the deleted version
helm uninstall releaseName --keep-history

# Automatically generates the release Name for the chart
helm install repoName/chartName --generate-name

# Deletes the installation process on failure
helm install releaseName repoName/chartName --atomic

# Creates the namespace if it is not present
# Deploy all the resources in the namespace while deploying
# During the uninstall process, created namespace will not delete automatically
# Only the resources in ns will delete
helm install releaseName repoName/chartName --n dev --create-namespace

# Dry run
helm install releaseName repoName/chartName --dry-run --debug
helm upgrade releaseName repoName/chartName --dry-run

# Provide custom values.yaml
helm upgrade releaseName repoName/chartName -f values.yaml --dry-run --debug

# provided values will list here
helm get values releaseName

# Used to create chart
helm create basechart

. -> Root Object
.Values, .Chart, .Release, .Files(provides access to all non special files in the chart), .Template (contains information about the current context template executing), .Capabilities (provides information about the kubernetes cluste)

NOTES.txt is rendered same as regular template file. It will display as command line output when we install the chart

# Locally render the manifest file without creating them
helm template name chartName

{{ default "MYRELEASE101" .Values.deploymentName }} #DEFAULT FUNCTION

template-in-template : used to call one named function inside another named function

# Used to create resources from the charts
helm install releaseName .

# Used to package the charts
helm package mychart/ --destination packages/

