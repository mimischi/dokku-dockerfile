# dokku-dockerfile

Deploy your applications via `Dockerfile`, while keeping your project root clean of auxiliary files.

## Installation

```
sudo dokku plugin:install https://github.com/mimischi/dokku-dockerfile.git
```

## Commands

```
dockerfile:set    <app> <path/to/Dockerfile> Set custom path to Dockerfile
dockerfile:unset  <app>                      Unset custom path to Dockerfile
dockerfile:report <app>                      Report custom path to Dockerfile
```

## Usage

Dokku will look for a `Dockerfile` in the project root, when building a
non-buildpack application. Depending on the projects structure, it's desirable
to keep deployment specific files in subdirectories. This plugin points Dokku
to the relative path of the `Dockerfile`.

To deploy an application with a directory structure as shown below, one would
use the following command:

```
dokku dockerfile:set <app> docker/dokku/Dockerfile
```

### Example project structure
```
.
├── app
│   ├── [...]
├── docker
│   ├── dokku
│   │   ├── Dockerfile
│   │   ├── [...]
│   └── local
│       ├── Dockerfile-dev
├── docker-compose.yml
└── README.md
```

## Behind the scenes

During the deploy process, this plugin copies the `Dockerfile` specified path to
the projects root, enabling Dokku to build it.
