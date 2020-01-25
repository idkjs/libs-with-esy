# libs-with-esy

[![Build Status](https://dev.azure.com/esy-ocaml/esy-ocaml/_apis/build/status/esy-ocaml.libs-with-esy?branchName=master)](https://dev.azure.com/esy-ocaml/esy-ocaml/_build/latest?definitionId=1?branchName=master)

A project which demonstrates a Reason workflow with [Esy][].

[Esy]: https://github.com/esy-ocaml/esy

[Native Workflow](https://reasonml.github.io/docs/en/quickstart-ocaml) found in link which we are trying to adhere to.

## Usage

```sh
➜  GitHub git clone https://github.com/esy-ocaml/hello-reason.git libs-with-esy
Cloning into 'libs-with-esy'...
remote: Enumerating objects: 47, done.
remote: Counting objects: 100% (47/47), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 1044 (delta 27), reused 21 (delta 9), pack-reused 997
Receiving objects: 100% (1044/1044), 260.62 KiB | 3.34 MiB/s, done.
Resolving deltas: 100% (534/534), done.
➜  GitHub cd libs-with-esy
➜  libs-with-esy [master]rm -rf .git
# at this point I search for `hello-reason` and changed it to `libs-with-esy` then changed `hello-reason.opam` and `hello-reason.install` to `libs-with-esy.opam` and `libs-with-esy.install`. See note just below.
➜  libs-with-esy [master]esy
info esy 0.6.0 (using package.json)
info fetching: done
info installing: done
➜  libs-with-esy [master]esy test
Running Test Program:
Hello, World!
```

Note: Changing the `package.json` name seems to break the project. Build system seems to be referring to it to build `.opam` files. Not very `get started` friendly if that is the case.

You need Esy, you can install the beta using [npm](https://npmjs.com):

    % npm install -g esy@latest

> NOTE: Make sure `esy --version` returns at least `0.5.4` for this project to build.

Then run the `esy` command from this project root to install and build dependencies.

    % esy

Now you can run your editor within the environment (which also includes merlin):

    % esy $EDITOR
    % esy vim

Alternatively you can try [vim-reasonml](https://github.com/jordwalke/vim-reasonml)
which loads esy project environments automatically.

After you make some changes to source code, you can re-run project's build
again with the same simple `esy` command.

    % esy

And test compiled executable (runs `scripts.tests` specified in
`package.json`):

    % esy test

Documentation for the libraries in the project can be generated with:

    % esy doc
    % esy open '#{self.target_dir}/default/_doc/_html/index.html'

Shell into environment:

    % esy shell


## Create Prebuilt Release:

`esy` allows creating prebuilt binary packages for your current platform, with
no dependencies.

    % esy npm-release
    % cd _release
    % npm publish

## Continuous Integration:
`libs-with-esy` includes CI configuration for Azure
[DevOps](https://dev.azure.com) pipelines out of the box.

- Create your Azure DevOps account.
- Add a new project, and point that new Azure DevOps project to your github
  repo that includes the CI (`./azure-pipelines.yml` and the `.ci/` directory)
  from `libs-with-esy`.
- Create a new Pipeline within that project.
  - When asked how to configure the new pipeline, select the option to use
    existing configuration inside the repo.

The CI is configured to build caches on the `master` branch, and also any
branch named one of (`global`, `release-*`, `releases-*`). That means that pull
requests to any branch with those names will be fast, once you have landed at
least one commit to that branch. The first time you submit a pull request to
one of those branches, the builds will be slow but then subsequent pull
requests will be faster once a pull request is merged to it.

