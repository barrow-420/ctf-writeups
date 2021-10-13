# SJTU VPN
## Ubuntu 20.04

SJTU Student VPN Configuration Guide
 for Ubuntu 20.04
    1 Demo System Configuration
Shell$ uname -a
5.4.0-77-generic
Shell$ lsb_release --all
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.2 LTS
Release:        20.04
Codename:       focal
    2 Procedure
        2.1 Install Relevant Packages
Install strongswan package using package manager. 
On Ubuntu, the command[1] can be
sudo apt install strongswan stongswan-swanctl
sudo apt install libstrongswan-extra-plugins libcharon-extra-plugins
        2.2 Import CA Certificates
The certificate from the servers providing the VPN service needs to be verified through proper CA certificates. For only the use of SJTU student VPN, no default certificates are installed with strongswan package, but openssl certificates are enough.
    1. Find the CA certificate folder cacert used by strongswan and the folder storing CA certificates certs used by openssl.
On Ubuntu, the folder cacert is located at /etc/ipsec.d/cacerts and the folder certs is located at /etc/ssl/certs.
    2. We use the certs provided by system. Several approaches are plausible.
Here, create soft links of the system certs to the strongswan folder cacert. 
sudo ln -s /etc/ssl/certs/* /etc/ipsec.d/cacerts/
        2.3 Create VPN Config and Establish Connection
Approach 1:  setting ipsec.conf and ipsec.secrets 
In the example[3], the VPN config, named sjtu-student, for a jAccount with user123 as its username and pass456 as its passphrase should be
    1. File /etc/ipsec.conf
conn "sjtu-student"
        keyexchange=ikev2
        left=%config
        leftsourceip=%config4,%config6
        leftauth=eap-peap

        right=stu.vpn.sjtu.edu.cn
        rightid=@stu.vpn.sjtu.edu.cn

        rightsubnet=0.0.0.0/0,2000::/3
        rightauth=pubkey
        eap_identity="user123"	# jAccount ID

        auto=add
        aaa_identity="@radius.net.sjtu.edu.cn"


    2. File /etc/ipsec.secrets
"user123" : EAP "password456"
Connect VPN by following command: 
sudo ipsec up "sjtu-student"
Disconnect VPN by following command: 
sudo ipsec down "sjtu-student"
Approach 2:  setting config file for swanctl 
On Ubuntu 20.04, the example file named sjtuvpn.conf for swanctl is located at:
 		/etc/swanctl/conf.d/sjtuvpn.conf .
In the example[3], the VPN config, named  sjtuvpn-student, for a jAccount with user123 as its username and pass456 as its passphrase should be
connections {
   sjtuvpn-student {
      vips = 0.0.0.0,::
      remote_addrs = stu.vpn.sjtu.edu.cn
      local {
         auth = eap-peap
         id = "user123"
         aaa_id = @radius.net.sjtu.edu.cn
      }
      remote {
         auth = pubkey
         id = @stu.vpn.sjtu.edu.cn
      }
      children {
         sjtuvpn-student {
            remote_ts = 0.0.0.0/0,::/0
         }
      }
      version = 2
      mobike = no
   }

secrets {
   eap-jaccount {
      id = "user123"
      secret = "pass456"
   }
}


Connect VPN by following commands: 
sudo swanctl -i --child sjtuvpn-student
Disconnect VPN by following commands: 
sudo swanctl -t --child sjtuvpn-student

        2.4 Configure (Enable/Start)[4] strongswan Daemon [5]
Start strongswan daemon (as service) possibly by following command:
sudo systemctl start strongswan-starter.service
If auto-start of the service on boot is needed, it can be achieved by following command:
sudo systemctl enable strongswan-starter.service
    3 Note
    1. The package openssl is only needed for CA certs. If required CA certs are manually imported, this package is not necessary.
    2. The leftauth setting in the template config also can be eap-mschapv2. (Other eap mode not tested)
    3. This example is mainly aimed to magnify that there are quotation marks in the setting eap_identity and the file ipsec.secrets.
    4. Start or enable the strongswan daemon will not connect to any configured VPN.
    5. This part may vary largely with different Linux distributions.
    4 Reference
    1. Virtual	IP	-	strongSwan	(https://wiki.strongswan.org/projects/ strongswan/wiki/VirtualIp)
    2. ipsec.conf: conn Reference - ipsec.conf: conn Reference - strongSwan (https:// wiki.strongswan.org/projects/strongswan/wiki/ConnSection)
    3. How to Setup an IKEv2 VPN Connection on Arch Linux (Example: NordVPN) :: rockyourcode (https://www.rockyourcode.com/how-to-setup-an-ikev2-vpnconnection-on-arch-linux-example-nordvpn/)
    4. 安卓系统strongswan应用配置VPN的方法-上海交通大学网络信息中心 (https:// net.sjtu.edu.cn/info/1076/2033.htm)
    5. 【学生VPN】Win8、Win10系统PowerShell配置方法上海交通大学网络信息中心 (https://net.sjtu.edu.cn/info/1076/2032.htm)
    6. strongSwan	-	ArchWiki	(https://wiki.archlinux.org/index.php/ StrongSwan#VPN_Variants)
    
    
   https://jachinshen.github.io/environment/2018/09/26/Linux%E4%B8%ADIKEv2%E6%96%B9%E5%BC%8FEAP%E8%BF%9E%E6%8E%A5VPN.html
   
   
   
