# Installing Metasploit

[Rapid 7 link](https://github.com/rapid7/metasploit-framework/wiki/Nightly-Installers)
```
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
  chmod 755 msfinstall && \
  ./msfinstall
  ```
Once installed, you can launch msfconsole as /opt/metasploit-framework/bin/msfconsole from a terminal window, or depending on your environment,
it may already be in your path and you can just run it directly.
On first run, a series of prompts will help you setup a database and add Metasploit to your local PATH if it is not already.

These packages integrate into your package manager and can be updated with the msfupdate command, or with your package manager. 
On first start, these packages will automatically setup the database or use your existing database.
