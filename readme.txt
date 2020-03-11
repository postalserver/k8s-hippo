Welcome to Postal.

The Postal web interface is available at the URL shown below.

  https://{{ config.domain }}

To find your SMTP server run the command below and look for the IP
assigned to the `smtp` service.

  hippo {{ stage-name }} status

To create an admin user run the following:

  hippo {{ stage-name }} console -c 'bin/postal make-user'
