1. Checkout Earthdata Drive from ECC
    ```
    git clone ssh://git@git.earthdata.nasa.gov:7999/drive/earthdata-drive.git
    ```

1. [Create an app at Earthdata Login](https://uat.urs.earthdata.nasa.gov/apps/new) (requires _Application Creator_ status)

    | Earthdata Login field | Example value |
    | ---- | ---- |
    | Application ID (UID) | `fakedaacdrive` |
    | Redirect URL | `https://testdrive.internal/urs-redirect` |
    | Client ID | Assigned by URS during registration |

1. Copy `override_vars.yml.example` to `override_vars.yml` and edit

    * Required values
        * `urs_app_name` is the Application ID (UID) on the app registration form
        * `urs_client_id` is the Client ID assigned by URS
        * `urs_auth_code` follows the HTTP Basic authentication scheme ("_uid_:_password_", base64-encoded)
            ```
            $ echo -n "fakedaacdrive:xxxxxxxxxxxx" | base64
            ZmFrZWRhYWNkcml2ZTp4eHh4eHh4eHh4eHg=
            ```

    * Other likely overrides
        * `drive_site_name` might need to be "localhost", with suitable `forwarded_port` changes to [`Vagrantfile`](Vagrantfile).
        * `urs_application_group` can be set to the ID of an application group in URS.
        * `urs_auth_server` can be set to a different URS server (eg, an instance of [Fake URS](https://git.earthdata.nasa.gov/projects/FAKEURS/repos/fake-urs/browse))

1. Go!
    ```
    vagrant up
    ```

1. Make sure that the value of `drive_site_name` (default is "testdrive.internal") resolves to the private network address of the virtual machine. Possibilities include:

    * [Vagrant Host Manager plugin](https://github.com/devopsgroup-io/vagrant-hostmanager)
    * Manually adjust `/etc/hosts` (on Linux, Macos)

1. Visit https://testdrive.internal/drive/
