#########
Diff ANSI
#########

Integrate external diff commands into Emacs for improved visualization.

Available via `melpa <https://melpa.org/#/diff-ansi>`__.


Motivation
==========

*This package aims to expose the best possible diff rendering, to save time and improve reading diff's in Emacs!*

When reading diff's, features such as side-by-side display, word-level changes and syntax highlighting
can help understanding the changes that have been made.

3rd party tools are available that support these features - this package aims to make those accessible within Emacs.

.. figure:: https://gitlab.com/ideasman42/emacs-diff-ansi/uploads/0dc4a85d55627707c801b002a8fc6ab0/diff-ansi-screenshot.png
   :scale: 50 %
   :align: center

   Screenshot of the ``diff-ansi`` used in Magit's log view.


Usage
=====

Currently there are two main uses for this package.

- You may run ``diff-ansi-buffer`` to display the current diff buffer.
- Enable ``diff-ansi-mode`` minor mode which installs hooks to use enhanced diff display for Magit's revision display.


Commands
--------

``diff-ansi-buffer``
   Create a new read-only buffer displaying diff contents from the current buffer.

``diff-ansi-mode``
   Enable a minor mode to use ``diff-ansi`` functionality where possible.


Customization
-------------

``diff-ansi-tool``: ``'delta``
   The external tool to use for displaying diffs.

   - `'delta <https://github.com/dandavison/delta>`__ supports side-by-side view, word level differences and syntax highlighting.
   - `'diff-so-fancy <https://github.com/so-fancy/diff-so-fancy>`__ supports word level differences.
   - `'ydiff <https://github.com/yinwang0/ydiff>`__ supports side-by-side view & word level differences.
   - ``'custom`` call a custom command using (``diff-ansi-tool-custom``).

``diff-ansi-extra-args-for-delta``
   Additional arguments to pass to delta.

``diff-ansi-extra-args-for-ydiff``
   Additional arguments to pass to delta.

``diff-ansi-tool-custom``
   The command to use when ``diff-ansi-tool`` is set to ``'custom``.

``diff-ansi-use-magit-revision-diff``
   Use ``diff-ansi`` when viewing commits in magit.

``diff-ansi-default-face``
   The background color of this face is used when no color is specified.

Advanced Customization
^^^^^^^^^^^^^^^^^^^^^^

Note that in general these settings can be left as-is,
but may be extended to adjust default behavior.

``diff-ansi-method``: ``'multiprocess``
   Method used for decoding ANSI sequences.

   - ``'immediate`` to convert immediate (blocking may be slow).
   - ``'progressive`` uses a timer (avoids blocking input).
   - ``'multiprocess`` to span multiple external processes for improved performance on large diffs.

``diff-ansi-chunks-size``: 8192
   The number of characters to process at a time for
   when ``diff-ansi-method`` is set to ``progressive`` or ``multiprocess``.

``diff-ansi-multiprocess-jobs``
   The number of processes to run simultaneously
   when ``diff-ansi-method`` is set to ``multiprocess``.


Details
=======

- Converting ANSI escape sequences can be slow for large diffs,
  this is why ``multiprocess`` support is default to avoid long wait times viewing diffs.


Installation
============

The package is available in melpa as ``diff-ansi``, here is an example with ``use-package``:

The package can be installed using ``straight``.

.. code-block:: elisp

   (use-package diff-ansi
     :commands (diff-ansi-mode diff-ansi-buffer)))
