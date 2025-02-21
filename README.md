# pg_ctl-auto-start
start postgres via asdf automatically

Find the full path to pg_ctl: $ asdf where postgres

Check the actual path of the PostgreSQL binary: To find the exact location of the pg_ctl binary, you can list the contents of the asdf installation directory: $ ls /home/"username"/.asdf/installs/postgres/16.6/

Edit the systemd service file: $ sudo nano /etc/systemd/system/postgresql-start.service

Copy and paste in the following text and make sure to change "username" to your name:
[Unit]
Description=Start PostgreSQL via ASDF
After=network.target

[Service]
Type=forking
User=b3ta
Group=b3ta
Environment=PATH=/home/"username"/.asdf/bin:/home/"username"/.asdf/installs/postgres/16.6/bin:$PATH
ExecStart=/home/"username"/.asdf/installs/postgres/16.6/bin/pg_ctl start -D /home/"username"/.asdf/installs/postgres/16.6/data
ExecStop=/home/"username"/.asdf/installs/postgres/16.6/bin/pg_ctl stop -D /home/"username"/.asdf/installs/postgres/16.6/data

[Install]
WantedBy=multi-user.target


Reload the systemd configuration: $ sudo systemctl daemon-reload

Start the service: $ sudo systemctl start postgresql-start.service

Check the status to ensure it started successfully: $ sudo systemctl status postgresql-start.service
