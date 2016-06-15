.. title:: Deployment

Deployment
==========

Introduction
------------

Deployments are handled automatically whenever possible so a combination of `DeployBot`_ and the
``rsync`` command is used for new projects and regular FTP/SFTP for older or legacy projects.

After setting up a project with DeployBot it'll help push changes automatically to the Staging
server whenever the repo is updated, for older projects changed files will need to be uploaded
manually.

.. danger::
    Changes **must not** be made directly on the live server.

.. _DeployBot: https://deploybot.com/

New projects
------------

A new project needs to be setup in DeployBot to handle automatic deployments, this is usually done
before starting to work on it. Most of the time only 2 servers need to be configured, Staging (or
ML Demo) and the Live server.

The process is very straightforward, there's an option to copy the settings from current projects so
that can be used to quickly configure most servers.

.. figure:: _static/copy.png
    :align: center

    Copy settings from Staging environment in DeployBot.

There's only a few things to keep in mind:

- For Staging servers the deployment mode can be set as **Automatic** but for Live server this must
  be set as **Manual**.
- Configuration specific files like ``local.xml`` or ``wp-config.php`` files are not tracked in the
  repo so the need to be set as **Configuration files** for each environment.

.. figure:: _static/deploy.png
    :align: center

    Manually deploy latest commits in DeployBot.

Legacy projects
---------------

Older or legacy projects are not tracked using DeployBot so deployments need to be handled manually
via FTP/SFTP.

To help with this the following bash commands can be used to get the files changed in a git repo:

.. code-block:: bash

    # Create archive of changed files in commit
    g2f () {
        if [ -z "$1" ]; then
            echo "Commit reference is required"
            return 1
        else
            git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $1 | xargs tar -rf ~/Desktop/diff.tar
        fi
    }

    # Create archive of changed files since commit
    g2ff () {
        if [ -z "$1" ]; then
            echo "Commit reference is required"
            return 1
        else
            git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT ${1}~..HEAD | xargs tar -rf ~/Desktop/diff.tar
        fi
    }

They can be used as:

- ``g2f COMMIT-SHA`` to get all the changed files in that commit.
- ``g2ff COMMIT-SHA`` to get all the changed files from that commit to the latest one.

Untracked assets
----------------

Some assets are not tracked in the repo but sometimes are necessary to include during the deployment
process, for example the ``media`` directory in Magento or ``uploads`` folder in WordPress.

``rsync`` can be user to upload these files to the target server, for example the following command:

.. code-block:: bash

    rsync -azP media/ mldemo:~/projects/magento/media

Will upload only the changed files in the local ``media`` folder to the one in the ML Demo server.

.. note::
    Each server needs to be setup in the local SSH config for the above command to work.
