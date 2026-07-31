<!--
SPDX-FileCopyrightText: 2023 Zextras <https://www.zextras.com>

SPDX-License-Identifier: AGPL-3.0-only
-->

<div align="center">
  <h1>Carbonio Preview DB</h1>
</div>

<div align="center">
Service sidecar used by Carbonio Preview to communicate with a centralized database

[![Contributors][contributors-badge]][contributors]
[![Activity][activity-badge]][activity]
[![License][license-badge]](COPYING)
[![Project][project-badge]][project]
[![Twitter][twitter-badge]][twitter]

</div>

## How to install 🏁

### Preparing the environment

- Install PostgreSQL: `apt install postgresql`
- Create a `postgres` superuser:
  ```bash
  # sudo -u postgres
  $ psql
  # CREATE ROLE "carbonio-adm" WITH LOGIN SUPERUSER encrypted password 'your-secret-password';
  # CREATE DATABASE "carbonio-preview-db" owner "carbonio-adm";
  # \q
  ```

### Installation

Install `carbonio-preview-db` via apt:

```bash
sudo apt install carbonio-preview-db
```

or via yum:

 ```bash
sudo yum install carbonio-preview-db
```  

### Configuration

In order to make it work with external databases the `carbonio-preview-db.hcl` **MUST** be manually
updated by changing the address from `127.0.0.1` to the remote address. To finalize the
configuration:

- Execute `pending-setups` in order to register the service in the `service-discover`
- Bootstrap the database:
  ```bash
  PGPASSWORD=your-secret-password carbonio-preview-db-bootstrap carbonio-adm 127.0.0.1
  ```

If the bootstrap script is executed multiple times it reuses the credentials created the first time
and stored in `service-discover`.

### Reading config values

All the necessary configurations are saved automatically in the `service-discover` configuration
system. They can be retrieved with the following commands:

- `consul kv get -token-file="/etc/carbonio/preview/service-discover/token" "carbonio-preview/database/credentials/db-name"`
- `consul kv get -token-file="/etc/carbonio/preview/service-discover/token" "carbonio-preview/database/credentials/db-username"`
- `consul kv get -token-file="/etc/carbonio/preview/service-discover/token" "carbonio-preview/database/credentials/db-password"`

## License 📚

Service sidecar used by Carbonio Preview to communicate with a centralized database.

Released under the AGPL-3.0-only license as specified here: [COPYING](COPYING).

Copyright (C) 2023 Zextras <https://www.zextras.com>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU Affero General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU Affero General Public License for more details.

    You should have received a copy of the GNU Affero General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.

See [COPYING](COPYING) file for the project license details

### Copyright notice

All non-software material (such as, for example, names, images, logos, sounds) is owned by Zextras
s.r.l. and is licensed under [CC-BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/).

Where not specified, all source files owned by Zextras s.r.l. are licensed under AGPL-3.0-only

[contributors-badge]: https://img.shields.io/github/contributors/zextras/carbonio-preview-db "Contributors"

[contributors]: https://github.com/zextras/carbonio-preview-db/graphs/contributors "Contributors"

[activity-badge]: https://img.shields.io/github/commit-activity/m/zextras/carbonio-preview-db "Activity"

[activity]: https://github.com/zextras/carbonio-preview-db/pulse "Activity"

[license-badge]: https://img.shields.io/badge/license-AGPL-blue.svg

[project-badge]: https://img.shields.io/badge/project-carbonio-informational "Project Carbonio"

[project]: https://www.zextras.com/carbonio/ "Project Carbonio"

[twitter-badge]: https://img.shields.io/twitter/follow/zextras?style=social&logo=twitter "Follow on Twitter"

[twitter]: https://twitter.com/intent/follow?screen_name=zextras "Follow Zextras on Twitter"
