## This is a basic guide for adding documentation to your Backstage application using techdocs.

Prerequisites:

- [Creating your Backstage App](https://backstage.io/docs/getting-started/)
- [Register your app as an existing component](https://backstage.io/docs/features/software-catalog/#adding-components-to-the-catalog)

At this point, you have an existing repository of your Backstage application, and you have also registered it as an existing component within your Backstage instance. let’s now add basic documentation.

Within your `app-config.yaml` file update the techdocs section to look like the following. since our documentation will be stored locally/within the repository:

```bash
techdocs:
  builder: 'local' # Alternatives - 'external'
  generator:
    runIn: 'local' # Alternatives - 'local'
  publisher:
    type: 'local' # Alternatives - 'googleGcs' or 'awsS3'. Read documentation for using alternatives.
```

Setting generator.runIn to local means you will have to make sure your environment is compatible with techdocs.

You will have to install the `mkdocs` and `mkdocs-techdocs-core` package from pip.

You can do so by including the following lines right above `USER node` of your `Dockerfile`:

```bash
RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

RUN pip3 install mkdocs-techdocs-core
```

Create a `mkdocs.yml` file in the root of your repository with the following content:

```bash
# Enter the site name of your app
site_name: 'research'
site_description: An informative description
plugins:
  - techdocs-core
  
# The nav names e.g. Prerequisite will be assigned their corresponding md files, these files are the documentation
nav:
  - Prerequisite: index.md
  - Team Tooling: team_tooling.md
  - Agile Training: agile_training.md
```

Update your component's entity description by adding the following lines to its `catalog-info.yaml` in the root of its repository:

```bash
metadata:
  annotations:
    backstage.io/techdocs-ref: dir:.
```

TechDocs uses the [`backstage.io/techdocs-ref` annotation](https://backstage.io/docs/features/software-catalog/well-known-annotations#backstageiotechdocs-ref) to download the documentation source files and generate an entity's TechDocs site.

Create a `/docs` folder in the root of your repository with at least an `index.md` file in it. *(If you add more markdown files, make sure to update the nav in the mkdocs.yml file to get proper navigation for your documentation.). For example, also add*  `team_tooling.md` and `agile_training.md` files. Also add markdown content into your files, for example in the docs/index.md you can write:

```bash
# example docs

This is a basic example of documentation.
```

Commit your changes, open up a pull request, and merge. You will now get your updated documentation next time you run Backstage!

## Reference

- [Creating and publishing your docs](https://backstage.io/docs/features/techdocs/creating-and-publishing#use-any-software-template)
