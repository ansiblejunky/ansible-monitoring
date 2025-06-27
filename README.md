# ansible-monitoring

Install and configure monitoring tools for managing Ansible Automation Platform.
This repository is different from what's available in that it uses podman to install and configure a container solution and not rpm installations.

- Grafana
- Prometheus

## Other things

Configure JSON in Grafana
- Navigate to Admin > Plugins and Install Grafana Infinity Datasource
- Navigate to Connections > Data Sources and create a new data source for Infinity plugin
- Configure the data source with the following settings:
  - Name: aap-gateway
  - Authentication: Basic Auth
  - User Name: admin
  - Password: admin
  - Allowed Hosts: https://<aap-gateway-ip>
  - Network > Skip TLS Verify: true
  - Health check URL: https://<aap-gateway-ip>/api/gateway/v1/ping/

Configure Prometheus in grafana
- Navigate to Connections > Data Sources and create a new data source for Prometheus
- Configure the data source with the following settings:
  - Name: prometheus
  - URL: http://host.containers.internal:9090

Podman logs:
- sudo journalctl -u container-prometheus logs
- sudo journalctl -u container-grafana logs
- sudo journalctl -u container-node_exporter logs

Refresh dashboard variables:
- Navigate to the dashboard and click on Edit button
- Click on the Settings in the top right
- Click on the Variables section
- Click on a variable to edit it
- Click on the "Run Query" button to refresh the variable
- Click on the "Save" button to save the changes

Create new node exporter dashboard:
- Navigate to Dashboards and import a new dashboard
- Use the dashboard ID 1860
- Click on the Import button
- Select the Prometheus data source
- Click on the Import button
- Click on the Save button to save the dashboard

TODO: Create node exporters for each AAP group
