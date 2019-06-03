egeneralov.jfrog-artifactory
============================

Provision artifactory installation. **WARNING**: not ready for production use.

Role Variables
--------------

- **ja_repo**: `deb https://jfrog.bintray.com/artifactory-pro-debs {{ ansible_distribution_release }} main`
- **ja_key**:
  - **server**: `keyserver.ubuntu.com`
  - **id**: `6B219DCCD7639232`
- **ja_manage_db**: `true`
- **ja_version**: `6.9.0`
- **ja_db**:
  - **type**: `postgresql`
  - **driver_version**: `42.2.5`
  - **host**: `127.0.0.1`
  - **port**: `5432`
  - **name**: `artifactory`
  - **user**: `artifactory`
  - **password**: `artifactory`
- **ja_database_vars**:
  - **pgdg_users**: `[]`
    - **user**: `{{ ja_db.user }}`
    - **password**: `{{ ja_db.password }}`
    - **database**: `{{ ja_db.name }}`

- **ja_initial_wizard**:
  - **version**: 1
  - **GeneralConfiguration**:
    **licenseKey**: `<base64>`
    **licenseKeys**: `[]`
    **baseUrl**: `https://mycomp.arti.co`
  - **OnboardingConfiguration**:
    - **repoTypes**: []

Dependencies
------------

- [egeneralov.nginx](https://github.com/egeneralov/ansible-nginx)

License
-------

MIT

Author Information
------------------

Eduard Generalov <eduard@generalov.net>
