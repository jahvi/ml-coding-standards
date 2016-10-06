.. title:: Site Assessments

Site Assessments
================

Sometimes we need to make site assessments on website we haven't built before
deciding to take them over, in general the main goal is to check the overall
quality of the website and see if we can work on it in the future. Some of the
things to look out for can be:

- **Magento version:** Check how old the Magento version is to see how much work it would take to update it if necessary.
- **Patches:** Check if all security patches have been applied, `Mage Report`_ can help to identify this.
- **Changes to core files**: Check if any of the core files have been changed, we can use the ``diff`` cli tool to quickly spot differences against a brand new Magento installation of the same version. The main folders to look are:

  - app/code/core/
  - app/design/frontend/base/
  - js/
  - lib/
  - shell/
  - skin/frontend/base/

- **Number of extensions installed**: Usually the more extensions installed the more likely it is that something will break.
- **Local file rewrites**: Check if some of the core classes have been overwritten in the **local** folder, specially important if any of the files need to be patched.
- **Overall code quality**: Check the code style, indentation, consistency, etc., most of the time if the code is written `the Magento way` it is easier to work with.

.. _Mage Report: https://www.magereport.com