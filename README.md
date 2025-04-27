BLS PRO Full Auto UserScript

This UserScript automates various steps of the BLS Spain Morocco online appointment booking process, aiming to simplify and potentially speed up the process of finding and securing an appointment slot. It works on the BLS website (www.blsspainmorocco.net) and integrates with Gmail (mail.google.com) to automatically retrieve OTP codes.

Disclaimer: Use this script responsibly and at your own risk. Automating interactions with websites may violate their terms of service and could potentially lead to account suspension. Website structure changes can break the script's functionality.
Features

    Automatic Login: Logs in using configured email and password.

    Automatic Captcha Solving: Integrates with pro.nocaptchaai.com to solve both Login and Appointment captchas automatically. (Requires an API key and a paid account on pro.nocaptchaai.com).

    Automatic Form Filling: Automatically selects Appointment Type, Category, Location, Visa Type, and Visa Sub Type based on your configuration.

    Automatic Slot Selection: If enabled, automatically selects an available appointment date and time slot (currently selects a random available slot).

    Automatic OTP Retrieval: Reads unread emails from blsspaingloral.com or blsinternation.com in your Gmail account to automatically extract and fill the OTP code.

    Configurable Auto-Submission: Allows you to enable or disable automatic form submission on various pages (Login, Captcha, Visa Type Selection, Slot Selection, Applicant Selection).

    Telegram Notifications: Sends a notification to a specific Telegram chat when the script checks for slots, indicating the configured location, category, visa type, and if slots are found. (Uses a hardcoded bot token and chat ID - see Configuration to change this).

    UI Enhancements: Hides preloaders, makes loaders dismissable, and adjusts page layout for better usability.

    On-Page Settings: Injects buttons on BLS pages to quickly change common settings like Category, Auto-submit Visa Type, and Auto-submit Slots directly in the browser.

Requirements

    Web Browser: A modern web browser supporting UserScripts (Chrome, Firefox, Edge, Brave, Opera, etc.).

    UserScript Manager: A browser extension like Tampermonkey, Violentmonkey, or Greasemonkey (Tampermonkey is generally recommended for full compatibility with @grant features).

    pro.nocaptchaai.com Account & API Key: Required for automatic captcha solving. You will need to purchase credits or a subscription from them. The API key must be inserted into the script code.

    Script Configuration: You must edit the script code to add your applicant details, pro.nocaptchaai.com API key, and optionally, your own Telegram bot details.

    Gmail Access: Ensure the Gmail account used for BLS notifications is accessible in the same browser where the script runs, and that emails from BLS are not filtered or spammed.

Installation

    Install a UserScript manager extension (e.g., Tampermonkey) in your browser.

    Click the Tampermonkey icon, then click "Create a new script...".

    Delete any default code provided in the new script editor.

    Copy the entire code block from this script (including the // ==UserScript== and // ==/UserScript== lines).

    Paste the copied code into the script editor.

    Crucially, configure the script by following the instructions in the Configuration section below.

    Save the script (File -> Save).

    Ensure the script is enabled in your UserScript manager dashboard.

Configuration

Configuration is done by editing the script code directly within your UserScript manager. Open the script in the editor and find the following sections:

    applicants Array:
    This is the most important part. You need to define the details for each applicant.
    Locate the applicants variable near the top:

          
    const applicants = [{
      name: 'said', // Optional: A friendly name for you
      mail: 'sa@GMAIL.COM', // Required: Your BLS account email
      password: '*19id*', // Required: Your BLS account password
      profilePhotoId: '', // Optional: You can fill this in after the first successful login if you know it
      applicantCount: 1, // Required: Number of applicants for this booking (1 for Individual, >1 for Family)
      category: 'normal', // Required: Booking category. Use 'n' or 'normal', 'pm' or 'premium', 'pt' or 'primetime'.
      location: 'rabat', // Required: Booking location. Use 'tet', 'nad', 'aga', 'rab', 'tan', 'cas' or their full names.
      visa: 'sch' // Required: Visa Type. Use 'sch', 'std', 'famr', 'nat', 'work', 'c1', 'c2', 'c3' or their full names.
    }];

        

    IGNORE_WHEN_COPYING_START

Use code with caution. JavaScript
IGNORE_WHEN_COPYING_END

    Modify the existing object or add new objects within the [] array for each BLS account you want to use.

    Ensure mail, password, applicantCount, category, location, and visa are filled correctly. Refer to the comments for valid values for category, location, and visa.

    profilePhotoId is less critical and might be automatically handled or can be ignored if the site doesn't strictly require pre-filling it.

    The script currently seems to only use the first applicant object in this array for login and form filling. If you have multiple users, you might need to manually switch accounts on the login page or modify the script's login logic.

autoSubmitForms Object:
Control which forms are automatically submitted after the script interacts with them.
Locate the autoSubmitForms variable:

      
const autoSubmitForms = {
  login: 'on', // 'on' to auto-click login button after filling email/password
  loginCaptcha: 'on', // 'on' to auto-click verify after solving login captcha
  appointmentCaptcha: 'off', // 'on' to auto-click verify after solving appointment captcha
  visaType: 'on', // 'on' to auto-click submit after selecting visa type details
  slotSelection: 'on', // 'on' to auto-click submit after selecting slot
  applicantSelection: 'on' // 'on' to auto-click submit after applicant details/OTP
};

    

IGNORE_WHEN_COPYING_START

    Use code with caution. JavaScript
    IGNORE_WHEN_COPYING_END

        Change the values to 'on' or 'off' as desired.

    Captcha API Key (pro.nocaptchaai.com):
    The script uses a hardcoded API key placeholder (kingiliass-12d97066-e6c1-dd28-5264-eefcb0cacaee). You must replace this with your actual API key from pro.nocaptchaai.com.
    Search for kingiliass-12d97066-e6c1-dd28-5264-eefcb0cacaee in the script. You should find it in two places within the _0x26fc42 (Login Captcha) and _0x2075f9 (Appointment Captcha) classes, inside the _solveCaptcha methods.
    Replace the placeholder string with your key: 'YOUR_NOCAPTCHAAI_API_KEY_HERE'.

    Telegram Notifications:
    The script sends notifications to a specific bot and chat ID.
    Search for api.telegram.org/bot7257088385:AAFnMPaniXnRdh5NK0BNFVkzgoiXvlAJabU/sendMessage and chat_id=-4796426844.

        7257088385:AAFnMPaniXnRdh5NK0BNFVkzgoiXvlAJabU is the bot token.

        -4796426844 is the chat ID.
        If you want to use your own bot and receive notifications in your own chat, you will need to:

        Create a new Telegram bot via @BotFather.

        Start a chat with your new bot and send it a message.

        Get your chat ID. You might need to temporarily add the bot to a group with @getmyid_bot or use the Telegram Bot API directly (https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates) after sending a message to your bot or group. Note that group chat IDs start with -.

        Replace the hardcoded token and chat ID strings in the _0x5d0f00 function with your own.

    On-Page Buttons:
    When you visit BLS pages (except Slot Selection and Applicant Selection), you'll see fixed buttons on the left side:

        Categoryspain: [Category]

        submitTVS (ON/OFF)

        submitslots (ON/OFF)

    Clicking these buttons will cycle through or toggle the respective settings stored in localStorage, overriding the values you might have set in the autoSubmitForms object for visaType and slotSelection, and controlling the category used. The state of these buttons persists across sessions.

How it Works

The script monitors the current URL. When you navigate to a specific page on blsspainmorocco.net or mail.google.com that the script is configured to handle, it executes the corresponding logic:

    BLS Pages: It waits for the page to load, modifies the UI, retrieves necessary data from the page (sometimes accessed directly via unsafeWindow), fills forms, interacts with page elements (like clicking buttons), and potentially solves captchas or triggers redirects.

    Gmail Page: It periodically scans the inbox for new unread emails from BLS, opens the relevant ones, extracts 6-digit codes, and passes them back to the BLS script using GM_setValue.

    Inter-Page Communication: It uses localStorage to persist settings (like category, auto-submit toggles) and GM_setValue/GM_addValueChangeListener to communicate the extracted OTP from Gmail to the BLS site.

Important Notes

    The captcha solving relies on a paid third-party service (pro.nocaptchaai.com). Without a valid API key and credits, the script will likely get stuck on captcha pages.

    The Telegram integration uses a hardcoded bot token and chat ID. Replace them with your own if you don't want to send notifications to the default target.

    The slot selection logic currently appears to pick a date and slot somewhat randomly from available options. It does not have logic to prefer specific dates or times.

    The script includes some code obfuscation (e.g., variable and function names starting with _0x). This makes it harder to read and modify.

    Any changes to the BLS website's structure, element IDs, class names, or JavaScript variables/functions could break the script's functionality.
