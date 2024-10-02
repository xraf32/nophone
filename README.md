# nophone
Replace phone by other devices where possible

## Why
<details><summary>1. A waste of money is a waste of life</summary><p>
  A $100 phone in USA costs 1 month of the average income in Brazil due to the abusive taxes. A law forbids banks to offer services to individuals without a phone app. Very convenient for the 4 big banks, which can afford Android and iOS development teams whereas small banks cannot. Without a phone, the individual cannot access its own money in the bank. With normal usage, the phone must be replaced every 2 years, but it can also be stolen way before that. Very convenient for the phone stores. How much of the lifespan of a human can be saved by extending the phone service life?
  1. Normie: $100 for 2 years = 0.5 average month of income per year = 4.2% of human lifespan

  2. Smart: buy an alarm clock, so the phone is turned off at night:

    (24-8) h/day + $5 for a clock that lasts 6 years + $1/year for batteries
    Phone service life: 2 years * 24 / (24 - 8) = 3 years
    Yearly cost: 100/3 + (5/6 + 1) $/year = 0.3516/12 months/year = 2.9 % of human lifespan

  3. Expert: smart + all of the following:
    a. only use phone 6 h/day, mostly in flight-mode
    b. keep GPS and bluetooth off most of the time
    c. cooled slow charging, no trickle charging
    d. debloated ROM like LineageOS

    Items a to c extend battery life so that it is no longer the limiting factor, which then
    becomes the software: updates increase the footprint while the hardware wears and tears.
    All items decrease wear & tear rate, but item d also decreases the baseline footprint.

    New baseline phone service life: 2 years * 24/6 = 8 years
    Extra life due to lower wear & tear rate (wild guess): 1 year
    Extra cost to setup items c and d: $80

    Yearly cost: (5/6 + 1) + (100 + 80)/(8+1) $/year = 0.2183/12 months/year = 1.8% of human lifespan

A simple and cheap clock saves 1.2% of human lifetime = phone price dropped to $69
A complex expensive setup saves only 1.1% more = phone price dropped further to $43
That makes sense: the closer to the optimum, the harder it is to improve, hence the
Paretto principle, the law of diminishing returns, the marginal cost/gain, etc.
  
</p></details>

<details><summary>2. OPSEC and privacy, ultimately freedom</summary><p>
  A loose piece of information is worthless for the higher slaves trying to scam, tax, censor, harm or control the lower slave. The phone ties together all the data the slave generates there to its identity and location, which makes it a goldmine to the higher slaves. The more the lower slave replaces its phone with devices under its full control in its daily routine, the more the lower slave turns the goldmine into a garbage dump.
  
</p></details>

</p></details>

<details><summary>3. flexibility, ultimately peace</summary><p>
  The lower slave decides how his devices work, not a higher slave worried about ad revenue and whatnot.
  
</p></details>

## How
### Parts
1. A computer with MX Linux, a USB microSD card reader/writter and a wired Ethernet RJ45 connection to a router (**recommended: admin access. Routers may block devices or not display info like their IP otherwise**)
2. An old Rock64 2gb board (dead platform. Was never used)
3. A 5V 3A power supply with a...<details><summary>strange connector:</summary><p>
    ```
    Spec: 3.5mm outer diameter, 1.35mm inner diameter.
    Thridworldian slaves don't understand the concept of specs.
    They describe this sometimes as 3.4x1.4 or even Mini P4.
    This is a thirdworldian example of correct spec:
    ```
    https://produto.mercadolivre.com.br/MLB-3729696460-fonte-carregador-5v-3a-notebook-positivo-motion-cruy-q464c--_JM
    </p></details>
4. A 32 gb microSD card
5. An extra RJ45 Ethernet cable to connect the Rock64 to the same network as the computer
6. A keyboard, mouse and HDMI monitor to do the first setup of the Rock64
7. An old set of stereo speakers (rarely used many years ago)
8. Some pushbuttons, resistors, wires

### Rock64 setup
1. Download DietPi image: https://dietpi.com/#downloadinfo -> select PINE64 -> select ROCK64
2. Download Balena Etcher: https://etcher.balena.io/
3. Use Balena to flash the DietPi Image into the SD card
4. Edit the file `/boot/dietpi.txt`: <details><summary>click to expand</summary><p>
    ```
    # this is a comment. Valid timezone strings: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
    AUTO_SETUP_TIMEZONE=Europe/London
    # unfortunately, the setting below does not work. Keyboard layout must be changed interactively after install...
    # AUTO_SETUP_KEYBOARD_LAYOUT=gb
    # automated install
    AUTO_SETUP_AUTOMATED=1
    # X server and XFCE
    AUTO_SETUP_INSTALL_SOFTWARE_ID=25
    # LightDM login mask
    AUTO_SETUP_AUTOSTART_TARGET_INDEX=16
    # xrdp
    AUTO_SETUP_INSTALL_SOFTWARE_ID=29
    # disable survey and don't ask about it. If the slave wants, the slave can re-enable this later.
    SURVEY_OPTED_IN=0
    ```
    </p></details>
5. Remove the SD from the computer and put it in the Rock64. Connect the keyboard, mouse, HDMI monitor and RJ45 cable. Only then connect the power supply
6. The Rock64 will boot. Use the keyboard, mouse and monitor to configure whatever is needed. For example, the default keyboard layout and passwords, and hostname. Default password is `dietpi`. In step 4, X and XFCE were installed. They can be tested with the command `startx`.
7. Find the IP of the Rock64 within the network: <details><summary>some ways to do this. In this example, it is `192.168.15.18`</summary><p>
   a. logout (`exit`) and login again in DietPi (default password: `dietpi`). This will be shown in the HDMI monitor:
   ![r64_setup2](https://github.com/user-attachments/assets/f1d77ec0-e9ff-48ac-9c32-453e552ab420)
   
   b. in DietPi, issue the command `ip a`:
   ![r64_setup3](https://github.com/user-attachments/assets/72ae5736-bf85-4d41-a3de-64e13a989d73)

    </p></details>
8. Go back to the computer, open a terminal and issue `ssh dietpi@192.168.15.18`, replacing `192.168.15.18` by the actual IP found in step 7. Type your DietPi password (default: `dietpi`). This is remote SSH access, a much easier way to control the Rock64. The keyboard, mouse and HDMI monitor are no longer needed and can be disconnected from the Rock64.
9. Test the internet connection and update the system:
    ```
    sudo apt update
    sudo apt full-upgrade
    ```
    <details><summary>Why the internet connection matters even if the slave will not use a web app</summary><p>
    
    A computer has an RTC clock powered by an independent battery, this is why its clock does not reset at every boot. An SBC like the Rock64 does not have this. DietPi corrects the time at every boot by syncing the system clock to an NTP server over the internet. So, without internet, the clock will be wrong. That will prevent HTTPS connections, but the error messages will not indicate the problem is the clock. To avoid this snowball of stupidity, it is easier to make sure the internet always works than to install an RTC module. Moreover, the setup for the internet is the same for SSH access, which is the best solution to interface with an SBC anyway.
   
    </p></details>
    
11. Without `sftp-server`, `scp` won't work to transfer files between the computer and Rock64. So install that package: `sudo apt install openssh-sftp-server`
12. 


