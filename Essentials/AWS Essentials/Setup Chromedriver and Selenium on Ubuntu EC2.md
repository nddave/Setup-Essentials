# Installing Chromedriver with Selenium on Python3 Ubuntu EC2

This setup will walk you through a step by step process of installing Chromedriver with Selenium web scraping library on AWS' EC2 machine preloaded with Ubuntu and Python3.

## Update Apt
We start by updating the APT on Ubuntu. Please note that ```-f``` is used to automatically installs the missing requirements.
```
$ sudo apt update
$ sudo apt -f install
$ sudo apt full-upgrade
```
At this point click ```Install the package maintainer's version``` option when prompted. Unless if you wish to do so otherwise.
```
$ sudo apt -f install
```
We have now successfully updated Apt.

## Install Chrome
Now we need to install the latest version of Chrome, in order to do so, we need to install dependencies that allow seamless installation of Chrome on Ubuntu.
```
$ sudo apt-get install libxss1 libappindicator1 libindicator7
```
After installing the dependencies, we can now go ahead and download Chrome.
```
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i google-chrome*.deb
$ sudo apt-get install -f
```
We have now successfully installed Chrome.

## Install xvfb
We now proceed to install xvfb. ```xvfb``` stands for x virtual framebuffer, it allows us to load GUI applications in a virtual environment such that they run "heedlessly". Meaning, without loading all unnecessary features of the UI.
```
$ sudo apt-get install xvfb
```
We have now successfully installed xvfb.

## Install Chromedriver
Finally we now install the Chromedriver. In this particular setup, I am installing Chromedriver v2.30 but more driver versions can be found [here](https://chromedriver.storage.googleapis.com/index.html).
```
$ sudo apt-get install unzip
$ wget -N https://chromedriver.storage.googleapis.com/2.30/chromedriver_linux64.zip
$ unzip chromedriver_linux64.zip
$ chmod +x chromedriver
$ sudo mv -f chromedriver /usr/local/share/chromedriver
$ sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
$ sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
```
We have now successfully installed Chromedriver.

## Install Pip
Install pip so to later install Selenium.
```
$ sudo apt-get install python3-setuptools
$ sudo easy_install3 pip
```
We have now successfully installed pip.

## Install Selenium and PyVirtualDisplay
PyVirtualDisplay allows Selenium to run webdrivers in a virtual display.
```
$ sudo pip3 install selenium
$ sudo pip3 install pyvirtualdisplay
```
We have now successfully installed Selenium and PyVirtualDisplay.

## Test code
Test the following code to ensure that everything works successfully. The code below will open Google on chrome, will wait for 5 seconds and should print success if everything executed well.
```Python
import selenium
import pyvirtualdisplay
import time

display = Display(visible=0, size=(800, 600))
display.start()
print('Display opened')

url = 'https://www.google.com'
driver = webdriver.Chrome()
print('Driver opened')
driver.get(url)
print('URL received')
time.sleep(5)
print('Success')

driver.quit()
print('Driver closed')
display.stop()
print('Display closed')
```

We have now successfully installed Chromedriver with Selenium, Python3 on AWS' Ubuntu EC2 machine.

# License information ![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
