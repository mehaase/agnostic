# Developers

## Making a tag

Enter the virtual env:

    $ poetry shell

From the virtualenv run:

    (venv) $ bumpver update --patch
    INFO    - fetching tags from remote (to turn off use: -n / --no-fetch)
    INFO    - Latest version from VCS tag: 1.0.2
    INFO    - Working dir version        : 1.0.2
    INFO    - Old Version: 1.0.2
    INFO    - New Version: 1.0.3
    INFO    - git commit --message 'Bump version 1.0.2 -> 1.0.3'
    INFO    - git tag --annotate 1.0.3 --message '1.0.3'

Choose from `--major`, `--minor`, and `--patch` version bumps. Use `git show head` to
review the proposed changes, then run the following to submit the tag to the repository:

    (venv) $ git push --follow-tags

## Making a release

Run the following commands to build and publish the package.

    $ poetry build
    $ poetry publish

For more details on authenticating to PyPI, [see
here](https://www.digitalocean.com/community/tutorials/how-to-publish-python-packages-to-pypi-using-poetry-on-ubuntu-22-04).
