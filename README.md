# Firewall-cmd
Install Firewalld on fedora:
Firewalld is usually pre-installed in Fedora. If not, you can install it using the package manager:
//commands
sudo dnf install firewalld
Start and enable Firewalld:

Start and enable the Firewalld service:
//command
sudo systemctl start firewalld
sudo systemctl enable firewalld
Create Zones:

Create the trusted-zone, internal-zone, and public-zone:

//command
sudo firewall-cmd --permanent --new-zone=trusted-zone
sudo firewall-cmd --permanent --new-zone=internal-zone
sudo firewall-cmd --permanent --new-zone=public-zone
Assign Interfaces to Zones:

Determine the interfaces corresponding to your trusted, internal, and public zones and replace "ethX", "ethY", and "ethZ" with the actual interface names.

//command
sudo firewall-cmd --permanent --zone=trusted-zone --add-interface=ethX
sudo firewall-cmd --permanent --zone=internal-zone --add-interface=ethY
sudo firewall-cmd --permanent --zone=public-zone --add-interface=ethZ
Set Zone Defaults:

Set the default policies for each zone. For example, to set the trusted-zone to accept, internal-zone to drop, and public-zone to drop:

command
sudo firewall-cmd --permanent --zone=trusted-zone --set-target=ACCEPT
sudo firewall-cmd --permanent --zone=internal-zone --set-target=DROP
sudo firewall-cmd --permanent --zone=public-zone --set-target=DROP

Define specific rules for each zone to allow or deny traffic based on your requirements. For example, to allow SSH in the trusted-zone:

sudo firewall-cmd --permanent --zone=trusted-zone --add-service=ssh
Reload Firewalld:

After making the changes, reload Firewalld to apply the new configurations:

sudo firewall-cmd --reload
Now, if all commands were executed successfully, you won't see any visible output. However, you can verify the changes by checking the status of the zones:

sudo firewall-cmd --get-zones
This command will display a list of all zones, including the ones you created (trusted-zone, internal-zone, and public-zone), along with their settings and interfaces. 
