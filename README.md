I will now be using nix and all of its wonderful capabilities in my repos going forward.

<u>Note to self</u>:

Devbox (with toybox) will be the primary personal development reproducible environment due to the low system overhead, but do not use any of the `devbox generate` commands. Instead, manually create your `.devcontainer` folder contents to adequately mimic the devbox-created environment with the relevant installed project items. 

The `.devcontainer` folder should only contain the `.devcontainer.json` file and not a separate `Dockerfile` from the project's deployment `Dockerfile`(s). The `.devcontainer.json` build.args property can pass in the relevant environment argument such that, for example, if 'dev' it should make create a development container that is like-for-like with the devbox-created environmnet and if 'prod', it should make an extremely light container that is ready for deployment. Docker buildkit should be explored to make this efficient. 

The project should therefore only have its own proper `Dockerfile`(s) and not anyone specific to the `.devcontainer` folder to enable reproducible environments in other OCI-compliant containers and for non-vscode IDEs. Windows users should still be able to reproduce the environment either by installing Docker Desktop or by leveraging devbox in their WSL. Other OCI-compliant containers should work with this approach (with minor tweaks where necessary).

Users with devbox and vscode installed can simply run the `devbox shell` within the project root folder and then `code .` to bring up vscode IDE with a fully functional project environment.