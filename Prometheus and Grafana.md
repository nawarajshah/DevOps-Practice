## How to Install Prometheus and Grafana on Ubuntu 22.04 LTS — Configure Grafana Dashboard

### Creating Prometheus System Users and Directory

	sudo useradd --no-create-home  --shell /bin/false prometheus
	
![](https://miro.medium.com/v2/resize:fit:1050/1*FVfLUFhQWLc7Z68jUOD5xg.png)

	sudo mkdir /etc/prometheus  
	sudo mkdir /var/lib/prometheus

![](https://miro.medium.com/v2/resize:fit:1050/1*W0SSXmXx2dSpWSRjmcyKAA.png)

Set the ownership of the **/var/lib/prometheus** directory

	sudo chown prometheus:prometheus /var/lib/prometheus

![](https://miro.medium.com/v2/resize:fit:1050/1*dqRLIRiq5TxK8xBSgCbXHw.png)

### Download Prometheus Binary File
You need to inside /tmp :
	
	cd /tmp/

Download the Prometheus setup using wget

	wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz

![](https://miro.medium.com/v2/resize:fit:1050/1*VzsL1EPFa7rZoWuObM_vaw.png)

Extract the files using tar

	tar -xvf prometheus-2.46.0.linux-amd64.tar.gz

![](https://miro.medium.com/v2/resize:fit:1050/1*IlxnQs1upL7Nbc_XraBIuw.png)

Move the configuration file and set the owner to the prometheus user

	cd prometheus-2.46.0.linux-amd64
	sudo mv console* /etc/prometheus
	sudo mv prometheus.yml /etc/prometheus
	sudo chown -R prometheus:prometheus /etc/prometheus

![](https://miro.medium.com/v2/resize:fit:1050/1*gCv_p0wL-KI510RgDX-qFA.png)

Move the binaries and set the owner

	sudo mv prometheus /usr/local/bin/
	sudo chown prometheus:prometheus /usr/local/bin/prometheus

![](https://miro.medium.com/v2/resize:fit:1050/1*hOrwVbv6kzMqYPTsfWUJ8g.png)

### Creating Prometheus Systemd file
Create the service file

	[Unit]
	Description=Prometheus
	Wants=network-online.target
	After=network-online.target
	
	[Service]
	User=prometheus
	Group=prometheus
	Type=simple
	ExecStart=/usr/local/bin/prometheus \
		— config.file /etc/prometheus/prometheus.yml \
		— storage.tsdb.path /var/lib/prometheus/ \
		— web.console.templates=/etc/prometheus/consoles \
		— web.console.libraries=/etc/prometheus/console_libraries
	
	[Install]
	WantedBy=multi-user.target

Reload systemd

	sudo systemctl daemon-reload

Start, Enable, Status Prometheus service

	sudo systemctl start prometheus
	sudo systemctl enable prometheus
	sudo systemctl status prometheus

Launch the Prometheus server by executing the following command:

	./prometheus –config.file=prometheus.yml (or) ./prometheus

**Verify Prometheus Installation:**

Open your web browser and access [http://server-ip-address:9090](http://localhost:9090/). If Prometheus is running correctly, you will see the Prometheus web interface.

![](https://miro.medium.com/v2/resize:fit:1050/1*hzq8ZE9YcVToOBXq2-fv6A.png)

### Installing Grafana

	sudo apt install -y apt-transport-https  
	wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -  
	echo  "deb https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

**Install Grafana**

Update the package list and install Grafana with the following commands:

	sudo apt-get  update  
	sudo apt-get install grafana

**Start Grafana:**

Enable and start the Grafana service:

	sudo systemctl enable --now grafana-server

**Access Grafana:**

Open your web browser and go to [http://your-server-ip:3000](http://localhost:3000/). You will be prompted to set up a new admin password. Follow the on-screen instructions to complete the setup.

![](https://miro.medium.com/v2/resize:fit:1050/1*hCWznlR6OiEnu5_S6xnPug.png)

Execute the following command to set the admin password to a new value:

	sudo systemctl stop grafana-server  
	sudo grafana-cli admin reset-admin-password <new_password>  
	sudo systemctl start grafana-server

Finally logged in the Grafana

![](https://miro.medium.com/v2/resize:fit:1050/1*o7vbcGzXujz79OE4SC_Wyw.png)

![](https://miro.medium.com/v2/resize:fit:1050/1*q9VMRIwiGEIcd14QxNJ5qg.png)

**Configure Prometheus as a Data Source:**

In the Grafana web interface, click on “Connections” > “Data Sources.” Add a new data source and choose Prometheus. Provide the URL of your Prometheus server (e.g.,  [http://server-ip:9090](http://localhost:9090/)) and save the configuration.

![](https://miro.medium.com/v2/resize:fit:1050/1*_e4Ur9QMA2G-mYaRqiA25A.png)

![](https://miro.medium.com/v2/resize:fit:1050/1*_e4Ur9QMA2G-mYaRqiA25A.png)

Click save and test. Create a new dashboard

![](https://miro.medium.com/v2/resize:fit:1050/1*-AKJrAs9b-giTlEjFDLZQQ.png)

![](https://miro.medium.com/v2/resize:fit:1050/1*5D07ci_DkAnLE3UpwDsPkA.png)

Add visualization — add data sources (already added prometheus)

**Finally set the sample dashboard**

![](https://miro.medium.com/v2/resize:fit:1050/1*_QB9tuGzOr26zuJX9md8oA.png)

