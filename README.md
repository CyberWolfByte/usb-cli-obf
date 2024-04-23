# CLI Obfuscation Techniques (Windows)

This project focuses on assessing two different techniques for obscuring the visibility of the Command Prompt (CMD) on Windows systems. The goal is to determine which method is more effective for minimizing the Command Prompt's visibility during an engagement, thereby reducing the chance of detection by the target user.

## Disclaimer

The tools and scripts provided in this repository are made available for educational purposes only and are intended to be used for testing and protecting systems with the consent of the owners. The author does not take any responsibility for the misuse of these tools. It is the end user's responsibility to obey all applicable local, state, national, and international laws. The developers assume no liability and are not responsible for any misuse or damage caused by this program. Under no circumstances should this tool be used for malicious purposes. The author of this tool advocates for the responsible and ethical use of security tools. Please use this tool responsibly and ethically, ensuring that you have proper authorization before engaging any system with the techniques demonstrated by this project.

## Prerequisites

- **Operating System**: Tested on Windows 10 x64, version 22H2, Kali Linux 2023.4
- **Payload Studio**: Tested with Payload Studio Pro version 1.3.1
- **DuckyScript Version**: DuckScript 3.0 Advanced
- **Hardware**: Hak5 USB Rubber Ducky (2022)

## Technique Analysis

### **TECHNIQUE 1: `Window Manipulation`**

**Use Case**: This could be used in a scenario where the attacker wants to run commands or applications without drawing attentionto the active window. By moving it out of sight, they reduce the chanceof detection while carrying out their activities.

```
ALT SPACE
DELAY 200
STRING m
DELAY 200
HOLD DOWNARROW
DELAY 6000
RELEASE DOWNARROW
ENTER
```

**Steps**:

1. **Access Window System Menu**: `ALT SPACE` is used to open the system menu of the active window. This menu typically includes options to minimize, maximize, move, resize, and close the window.
2. **Select "Move" Option**: `STRING m` selects the "Move" option from the system menu. This choice depends on the assumption that "m" is the shortcut for the move option in the system menu, which is common in Windows environments.
3. **Move Window**: `HOLD DOWNARROW` then `RELEASE DOWNARROW` after a delay of 6 seconds moves the window downwards. This action could effectively move the window off the visible screen area, making it harder for a casual observer to notice any activities within the window.
4. **Finalize Position**: `ENTER` finalizes the move, setting the window's new position.

**Pros**:

- Effectively moves the Command Prompt window out of the user's visible screen area, making it less likely to be noticed.
- Does not alter the appearance of the Command Prompt, which might be less suspicious if seen briefly.

**Cons**:

- The window can be accidentally revealed if the user interacts with the taskbar or uses specific window management shortcuts.
- Requires precise timing to ensure the window is moved sufficiently off-screen without being completely inaccessible for further interactions.

### **TECHNIQUE 2: `Command Prompt Appearance Modification`**

**Use Case**: This technique could be utilized to execute commands in a less detectable manner. By altering the Command Prompt's appearance, the attacker aims to minimize the likelihood of the Command Prompt window drawing attention. The combination of a hard-to-read color scheme and a minimized window size could allow the execution of commands without alerting the user or passersby.

```
STRINGLN color FE
STRINGLN mode con:cols=14 lines=1
```

**Steps**:

1. **Open Run Dialog**: `GUI r` opens the Run dialog.
2. **Run as Administrator**: Executes `powershell Start-Process cmd -Verb runAs` to start a command prompt as an administrator.
3. **Bypass UAC**: `ALT y` confirms the UAC prompt automatically.

**Pros**:

- Significantly reduces the Command Prompt's visual footprint on the screen, making it less noticeable at a glance.
- The color change can make text difficult to read, further reducing the likelihood of someone understanding what's being executed if they do notice the window.

**Cons**:

- The window remains on-screen, albeit in a less conspicuous form. Sharp-eyed users might still notice and investigate the unusual window.
- Changing the window's size and color could arouse suspicion if observed, as these are not default settings for the Command Prompt.

### Comparative Evaluation

Both techniques have their merits and potential drawbacks. The choice between them should be informed by the operational requirements, including the level of stealth needed and the likelihood of target interaction with the computer during the operation.

- **For environments where physical surveillance by the target is a concern**, and the aim is to execute commands without attracting any attention to the Command Prompt window, **Technique 1** might be preferable. It effectively removes the window from the user's view, albeit with some risk of accidental rediscovery.
- **When stealthiness is less of a concern**, or if there's a high confidence that the target user will not closely inspect unusual windows on their screen, **Technique 2** offers a simple and quick way to make the Command Prompt less noticeable and harder to read, without completely removing it from view.
