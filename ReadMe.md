ssh-askpass for Mac OS
========================

MacOS's Signed System Volume makes it hard to modify settings of ssh-agent in
/System/Library/LaunchAgents/com.openssh.ssh-agent.plist

- https://support.apple.com/guide/security/signed-system-volume-security-secd698747c9
- https://grafxflow.co.uk/blog/mac-os-x/delete-ioplatformpluginfamilykext-macos-big-sur

My workaround is provided here:

*   Add these two options to ~/.ssh/config

        UseKeychain=no
        AddKeysToAgent=ask
        # AddKeysToAgent=confirm may cause mysterious signing failure

*   Run this command in your shell:

        export SSH_ASKPASS=/absolute/path/to/ssh-askpass

*   Environment variables as options:

        export SSH_ASKPASS_GUI=[ON|OFF]           # default: auto on
        export SSH_ASKPASS_TIMEOUT=[<seconds>]    # default: 3 minutes
        export SSH_ASKPASS_CACHETIME=[<seconds>]  # default: 15 minutes

It will fall back to GUI if interactive input from terminal is unavailable.

This program works on Mac OS 10.15+ and requires no third-party dependencies.
