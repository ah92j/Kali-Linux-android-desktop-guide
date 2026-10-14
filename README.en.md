<h1 align="left" dir="ltr">Run Kali Linux on Android from Scratch</h1>

<p align="left" dir="ltr"><strong>Termux + Kali NetHunter Rootless + TigerVNC + VNC Viewer + Fluxbox + tint2 + iDesk + code-server</strong></p>

<p align="left" dir="ltr">This guide walks through installing Kali Linux on an unrooted Android phone, setting up a lightweight desktop, and opening a VS Code-like editor in the phone browser.</p>

<p align="left" dir="ltr"><strong>How to use this guide:</strong> Read the explanation first. Each command is in its own left-to-right box. Copy only the command inside the box and paste it into the app named in the explanation. Run commands one at a time and wait for each to finish. Do not paste the box label or explanatory text into the terminal.</p>

<p align="left" dir="ltr"><a href="README.md">Arabic guide</a> · <a href="index.html">Arabic web guide</a></p>

<p align="left" dir="ltr"><strong>Important:</strong> Package names and details can vary across Android, Termux, and Kali versions. No guide can guarantee zero errors on every device. If a command fails, stop and copy the full error before trying other commands.</p>

<h2 align="left" dir="ltr">What you will set up</h2>

<ul align="left" dir="ltr">
<li>Kali Linux inside Termux without rooting the phone.</li>
<li>A graphical desktop using TigerVNC and VNC Viewer.</li>
<li>Fluxbox with the tint2 panel and iDesk desktop shortcuts.</li>
<li>A work folder at <code dir="ltr">~/Desktop/Python</code>.</li>
<li>code-server, a VS Code-like editor that runs in the phone browser.</li>
</ul>

<h2 align="left" dir="ltr">Before you start</h2>

<ul align="left" dir="ltr">
<li>An Android phone with several gigabytes of free storage. The final size depends on the packages and release.</li>
<li>A stable internet connection; keeping the phone on a charger during installation is recommended.</li>
<li>Install Termux from one official source only. Do not mix app or add-on builds signed by different sources.</li>
<li>This is a Rootless setup. It does not require root, but it cannot provide every feature of Kali on a rooted or native Linux device.</li>
<li>VNC and code-server will bind to <code dir="ltr">127.0.0.1</code>. Do not change this to <code dir="ltr">0.0.0.0</code>.</li>
</ul>

<h2 align="left" dir="ltr">Step 1: Install the apps</h2>

<p align="left" dir="ltr">Install Termux from one of these official sources. Choose only one:</p>

<ul align="left" dir="ltr">
<li><a href="https://f-droid.org/en/packages/com.termux/">Termux on F-Droid</a></li>
<li><a href="https://github.com/termux/termux-app/releases">Official Termux releases</a></li>
</ul>

<p align="left" dir="ltr">Also install VNC Viewer from a trusted app store. This guide uses TigerVNC inside Kali with VNC Viewer. Do not run KeX at the same time as the manual TigerVNC setup described here.</p>

<p align="left" dir="ltr"><strong>If Termux is already installed and working, do not uninstall it.</strong> Uninstalling may delete its local environment and files.</p>

<h2 align="left" dir="ltr">Step 2: Prepare Termux</h2>

<p align="left" dir="ltr">Open the original Termux app on Android, not a terminal inside Kali. Update its packages:</p>

<p align="left" dir="ltr"><strong>Where: the original Termux app.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkg update &amp;&amp; pkg upgrade -y</code></pre>

<p align="left" dir="ltr">Grant access to phone storage if Android asks for permission:</p>

<p align="left" dir="ltr"><strong>Where: Termux. Tap Allow if Android shows a permission dialog.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>termux-setup-storage</code></pre>

<p align="left" dir="ltr">Install the download utility:</p>

<p align="left" dir="ltr"><strong>Where: Termux.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkg install -y wget</code></pre>

<h2 align="left" dir="ltr">Step 3: Install Kali NetHunter Rootless</h2>

<p align="left" dir="ltr">Run these three commands in the original Termux app, in order. Copy one box at a time and wait for each command to finish.</p>

<p align="left" dir="ltr"><strong>Command 1 — download the installer.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>wget -O install-nethunter-termux https://offs.ec/2MceZWr</code></pre>

<p align="left" dir="ltr"><strong>Command 2 — make the installer executable.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>chmod +x install-nethunter-termux</code></pre>

<p align="left" dir="ltr"><strong>Command 3 — start installation. Follow any prompts and wait for the download and extraction to finish.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>./install-nethunter-termux</code></pre>

<p align="left" dir="ltr">Do not force-stop Termux during installation. It can take time depending on network speed and available storage.</p>

<p align="left" dir="ltr">After installation completes, start Kali with:</p>

<p align="left" dir="ltr"><strong>Where: Termux. You should now be at a Kali terminal prompt.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nethunter</code></pre>

<h2 align="left" dir="ltr">Step 4: Update Kali and install packages</h2>

<p align="left" dir="ltr">Make sure you are inside Kali. Update the system and wait for the process to finish:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali after running nethunter.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt update &amp;&amp; sudo apt full-upgrade -y</code></pre>

<p align="left" dir="ltr">Install the desktop, VNC server, and required tools:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. This may take a while.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt install -y fluxbox tint2 idesk xterm dbus-x11 tigervnc-standalone-server thunar feh adwaita-icon-theme x11-xserver-utils fonts-noto-core python3 python3-pip git curl wget ca-certificates xdg-utils</code></pre>

<p align="left" dir="ltr">If the package manager reports that a package cannot be found, do not guess alternative package names. Save the full error and check the package name available for your Kali release.</p>

<h2 align="left" dir="ltr">Step 5: Create work folders and configure the desktop</h2>

<p align="left" dir="ltr">Create configuration folders and the Python work folder:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p ~/.config/tigervnc ~/.idesktop ~/.config/tint2 ~/.fluxbox ~/.local/bin ~/Desktop/Python</code></pre>

<p align="left" dir="ltr">Create the desktop startup file. This command writes the whole configuration file, so copy the entire box at once:</p>

<p align="left" dir="ltr"><strong>Desktop startup configuration — inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>cat &gt; ~/.config/tigervnc/xstartup &lt;&lt;&#x27;EOF&#x27;
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
xsetroot -solid &quot;#4b2e69&quot; 2&gt;/dev/null
exec dbus-launch --exit-with-session sh -c &#x27;tint2 &amp; idesk &amp; exec fluxbox&#x27;
EOF</code></pre>

<p align="left" dir="ltr">Make the file executable:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>chmod +x ~/.config/tigervnc/xstartup</code></pre>

<p align="left" dir="ltr">This setup uses a purple background, Fluxbox, tint2, and iDesk. If your desktop already works with different settings, back up those settings before replacing them.</p>

<h2 align="left" dir="ltr">Step 6: Set a VNC password and start the server</h2>

<p align="left" dir="ltr">Create a password dedicated to VNC. The terminal will ask you to enter and confirm it. Never share it or put it in project files:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. If this command is not found, try the alternative below.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncpasswd ~/.config/tigervnc/passwd</code></pre>

<p align="left" dir="ltr"><strong>Alternative if tigervncpasswd is unavailable.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>vncpasswd ~/.config/tigervnc/passwd</code></pre>

<p align="left" dir="ltr">Start VNC on display 1 and restrict access to the phone itself:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. If it says a session is already running, do not start multiple sessions.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p align="left" dir="ltr">If an old session is stuck or you need to restart it, stop display 1 and start it again:</p>

<p align="left" dir="ltr"><strong>Stop the old VNC session — inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver -kill :1</code></pre>

<p align="left" dir="ltr"><strong>Restart the VNC session — inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p align="left" dir="ltr">Do not run KeX alongside the manual TigerVNC server; use one desktop-server path to avoid session conflicts.</p>

<h2 align="left" dir="ltr">Step 7: Connect using VNC Viewer</h2>

<ol align="left" dir="ltr">
<li>Open VNC Viewer on the phone.</li>
<li>Add a new connection.</li>
<li>Enter <code dir="ltr">127.0.0.1:5901</code> as the address.</li>
<li>Connect and enter the VNC password you created in the previous step.</li>
</ol>

<p align="left" dir="ltr">If the connection succeeds, you should see the Fluxbox desktop. Keep Termux running in the background while using VNC. If Android stops it automatically, check battery settings and allow Termux to run in the background if that option is available.</p>

<h2 align="left" dir="ltr">Step 8: Understand the desktop and create the Python folder</h2>

<ul align="left" dir="ltr">
<li><strong>Fluxbox:</strong> window and menu manager.</li>
<li><strong>tint2:</strong> taskbar panel.</li>
<li><strong>iDesk:</strong> displays desktop shortcuts defined by separate files.</li>
</ul>

<p align="left" dir="ltr">The work folder was created earlier. Verify that it exists:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Both Desktop and Python paths should be listed.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -ld ~/Desktop ~/Desktop/Python</code></pre>

<p align="left" dir="ltr">Note: iDesk does not automatically display folders like some desktop environments. If Python does not appear as an icon, the folder may still exist; create a shortcut in a separate step.</p>

<h2 align="left" dir="ltr">Step 9: Install code-server</h2>

<p align="left" dir="ltr">The desktop VS Code application failed in this PRoot environment because it could not access some system files. This guide therefore uses code-server, a VS Code-like editor that runs in the phone browser.</p>

<p align="left" dir="ltr">Download the official installation script to a file first:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>curl -fsSL https://code-server.dev/install.sh -o /tmp/code-server-install.sh</code></pre>

<p align="left" dir="ltr">Run the installer:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. It may ask for your sudo password to install the package.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sh /tmp/code-server-install.sh</code></pre>

<p align="left" dir="ltr">Verify that it was installed:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. A version number should appear.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>code-server --version</code></pre>

<h2 align="left" dir="ltr">Step 10: Start the editor and open the Python folder</h2>

<p align="left" dir="ltr">Copy the full command block into Kali. It creates the work folder if needed and starts the editor in the background, bound only to the phone:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Paste all three lines together.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p &quot;$HOME/Desktop/Python&quot;
nohup code-server --bind-addr 127.0.0.1:8080 &quot;$HOME/Desktop/Python&quot; &gt; &quot;$HOME/code-server.log&quot; 2&gt;&amp;1 &amp;
sleep 3</code></pre>

<p align="left" dir="ltr">Display the password locally on your phone:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Do not share the password or save it in a public project.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>grep &#x27;^password:&#x27; &quot;$HOME/.config/code-server/config.yaml&quot;</code></pre>

<p align="left" dir="ltr">Open the phone browser and enter this address in its address bar:</p>

<p align="left" dir="ltr"><strong>This is a browser address, not a terminal command.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>http://127.0.0.1:8080</code></pre>

<p align="left" dir="ltr">Enter the password shown in the terminal. The VS Code-like interface should open with the Python work folder ready in the file explorer. Create a new file in Explorer when you want to write a program.</p>

<p align="left" dir="ltr">If the editor does not open, inspect the latest log messages:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Save the error text if you need help.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tail -n 40 &quot;$HOME/code-server.log&quot;</code></pre>

<p align="left" dir="ltr">Keep the server bound to <code dir="ltr">127.0.0.1</code> for local use. Do not change it to <code dir="ltr">0.0.0.0</code> unless you understand the risk of exposing the editor to other devices.</p>

<h2 align="left" dir="ltr">Step 11: Add a Python shortcut to the desktop</h2>

<p align="left" dir="ltr">The following command creates a shortcut that opens code-server in the browser. code-server must be installed, but it does not need to be running while the icon is created.</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Copy the entire block exactly as shown.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p ~/.idesktop
ICON=&quot;$(find /usr/share/icons /usr/share/pixmaps -type f -iname &#x27;folder.png&#x27; -print -quit 2&gt;/dev/null)&quot;
if [ -z &quot;$ICON&quot; ]; then
  ICON=&quot;$(grep -hm1 &#x27;Icon:&#x27; ~/.idesktop/*.lnk 2&gt;/dev/null | sed &#x27;s/^[[:space:]]*Icon:[[:space:]]*//&#x27; | head -n 1)&quot;
fi
if [ -z &quot;$ICON&quot; ]; then
  echo &quot;No PNG icon found. Keep using code-server from the browser.&quot;
else
  cat &gt; ~/.idesktop/Python.lnk &lt;&lt;EOF
table Icon
  Caption: Python
  Command: xdg-open http://127.0.0.1:8080
  Icon: $ICON
  Width: 48
  Height: 48
  X: 180
  Y: 320
end
EOF
  echo &quot;Python shortcut created.&quot;
fi</code></pre>

<p align="left" dir="ltr">Restart iDesk so it reloads the shortcut:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. The desktop icons may disappear for a moment and then return.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkill -x idesk 2&gt;/dev/null || true
nohup idesk &gt;/tmp/idesk.log 2&gt;&amp;1 &amp;</code></pre>

<p align="left" dir="ltr">When the Python icon appears, double-tap it. It opens the editor address in the browser. If the icon does not appear, check that the shortcut file exists:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -l ~/.idesktop/Python.lnk</code></pre>

<h2 align="left" dir="ltr">Step 12: Hide the search bar at the top of the editor</h2>

<p align="left" dir="ltr">If the bar covering the top area is the Command Center, open the editor command palette and search for <code dir="ltr">Preferences: Open User Settings (JSON)</code>. Add the following setting inside the JSON object. Do not delete other settings already present:</p>

<p align="left" dir="ltr"><strong>JSON setting — add a comma as needed based on the surrounding settings.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>&quot;window.commandCenter&quot;: false</code></pre>

<p align="left" dir="ltr">If other settings are present, make sure commas are correct; invalid JSON can prevent the settings file from loading.</p>

<h2 align="left" dir="ltr">Optional: Try desktop VS Code</h2>

<p align="left" dir="ltr">This is optional and is not required. code-server is the recommended path for this phone. In the documented test, desktop VS Code installed but failed at launch because PRoot restricted access to system files. If you still want to try installing it, run these commands inside Kali:</p>

<p align="left" dir="ltr"><strong>Command 1 — install tools needed to add the repository.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt install -y wget gpg</code></pre>

<p align="left" dir="ltr"><strong>Command 2 — add the official Microsoft repository key.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/microsoft.gpg</code></pre>

<p align="left" dir="ltr"><strong>Command 3 — configure the official repository.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>printf &#x27;Types: deb\nURIs: https://packages.microsoft.com/repos/code\nSuites: stable\nComponents: main\nArchitectures: amd64,arm64,armhf\nSigned-By: /usr/share/keyrings/microsoft.gpg\n&#x27; | sudo tee /etc/apt/sources.list.d/vscode.sources &gt;/dev/null</code></pre>

<p align="left" dir="ltr"><strong>Command 4 — update package lists and install VS Code.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt update &amp;&amp; sudo apt install -y code</code></pre>

<p align="left" dir="ltr">If errors appear such as <code dir="ltr">Failed to initialize cpuinfo</code>, <code dir="ltr">Failed to read /proc/sys/fs/inotify/max_user_watches</code>, or <code dir="ltr">trace trap</code>, use code-server instead of disabling Electron security isolation. Disabling that isolation is not recommended as a permanent setup.</p>

<h2 align="left" dir="ltr">Daily startup</h2>

<ol align="left" dir="ltr">
<li>Open the original Termux app.</li>
<li>Start Kali using the command below, if you are not already inside Kali:</li>
</ol>

<p align="left" dir="ltr"><strong>Where: Termux.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nethunter</code></pre>

<p align="left" dir="ltr">If the VNC server is not running, start it inside Kali:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali. Do not run it again if the session is already active.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p align="left" dir="ltr">Open VNC Viewer and connect to <code dir="ltr">127.0.0.1:5901</code>. If code-server is stopped, start it inside Kali:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nohup code-server --bind-addr 127.0.0.1:8080 &quot;$HOME/Desktop/Python&quot; &gt; &quot;$HOME/code-server.log&quot; 2&gt;&amp;1 &amp;</code></pre>

<p align="left" dir="ltr">Then open <code dir="ltr">http://127.0.0.1:8080</code> in the phone browser. To stop the VNC session when finished, run this inside Kali:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver -kill :1</code></pre>

<h2 align="left" dir="ltr">Common troubleshooting steps</h2>

<h3 align="left" dir="ltr">VNC Viewer cannot connect</h3>

<p align="left" dir="ltr">Make sure the server is running and the address is <code dir="ltr">127.0.0.1:5901</code>. If an existing session is reported, do not create several sessions; stop the old session and restart it if needed.</p>

<h3 align="left" dir="ltr">The desktop is blank or icons are missing</h3>

<p align="left" dir="ltr">Inspect the startup file and its executable permission:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -l ~/.config/tigervnc/xstartup
cat ~/.config/tigervnc/xstartup</code></pre>

<p align="left" dir="ltr">iDesk may not show folders automatically. Create the Python shortcut as described in Step 11.</p>

<h3 align="left" dir="ltr">code-server does not open</h3>

<p align="left" dir="ltr">Check the version and inspect the log:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>code-server --version
tail -n 40 &quot;$HOME/code-server.log&quot;</code></pre>

<h3 align="left" dir="ltr">Thunar crashes while opening a folder or previewing an image</h3>

<p align="left" dir="ltr">In some PRoot environments, image previews can fail because of bwrap or Glycin sandbox restrictions. This does not mean the folder is missing. Do not disable the sandbox by default; check whether the work folder exists:</p>

<p align="left" dir="ltr"><strong>Where: inside Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -ld &quot;$HOME/Desktop&quot; &quot;$HOME/Desktop/Python&quot;</code></pre>

<h3 align="left" dir="ltr">A command or package is not found</h3>

<p align="left" dir="ltr">Make sure you are using the correct app: <code dir="ltr">pkg</code> commands belong in Termux, and <code dir="ltr">apt</code> commands belong inside Kali. Copy the full error and check official documentation before changing settings.</p>

<h2 align="left" dir="ltr">Security notes</h2>

<ul align="left" dir="ltr">
<li>Do not share the VNC or code-server password or upload secret configuration files.</li>
<li>Keep VNC and code-server bound to <code dir="ltr">127.0.0.1</code> for local use.</li>
<li>Do not disable Electron or Glycin sandboxing as a permanent workaround.</li>
<li>Do not place passwords or personal logs in a public project folder.</li>
</ul>

<h2 align="left" dir="ltr">Official references</h2>

<ul align="left" dir="ltr">
<li><a href="https://www.kali.org/docs/nethunter/nethunter-rootless/">Kali NetHunter Rootless documentation</a></li>
<li><a href="https://github.com/termux/termux-app#installation">Official Termux installation methods</a></li>
<li><a href="https://f-droid.org/en/packages/com.termux/">Termux on F-Droid</a></li>
<li><a href="https://manpages.debian.org/trixie/tigervnc-standalone-server/tigervncserver.1.en.html">TigerVNC documentation</a></li>
<li><a href="https://code-server.dev/">Official code-server website</a></li>
</ul>

<hr>

<p align="left" dir="ltr"><strong>This is a community guide, not an official Kali Linux or Termux release. Check the official documentation when package names or versions change.</strong></p>
