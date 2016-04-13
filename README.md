# cytoscape-manual
###Development version of Cytoscape user manual

This project is the working copy of the Cytoscape user manual. It will become the permanent manual once we have created a feature-complete and format-complete version. The outstanding issues are:

1. Table formatting using centralized CSS (mostly done)

2. Links within the document resolving properly
 
3. Links from outside of the document resolving properly

4. A proper placement of First pages, Table of Contents, and Document body
 
5. Typos introduced by the conversion process

4. A properly formatted PDF file

5. Incorporating the PDF file into the Cytoscape build process

While the manual sources are maintained in GitHub, the document is actually assembled, formatted, and staged by the ReadTheDocs.org site. ReadTheDocs presents online and PDF versions, and we will use both.

## Editing the Manual
To edit manual text, you must first check out this repository and use a text editor on your workstation. (You can use GitHub's native Markdown editor, too, for small edits.)

All document components are in the "docs" directory. Each chapter is contained in its own file, and the files are assembled as a complete document by naming them in the "docs/index.rst" file.

Images are stored in the "docs/_static/images" directory, organized into subdirectories by chapter. For high quality images, vector graphic files produce best results (e.g., .png).

Simple tables can be represented in Markdown, but high quality formatting requires direct HTML coding. By convention, we encode tables as tagged data, but do not specify visual attributes and layout inline. Instead, we use preset table styles contained in "docs/_static/css" for formatting. Note that additional CSS files can be added, but must be accounted for in "_templates/layout.html" and "conf.py".

Note that GitHub displays files containing Markdown with reasonably good quality. However, it only approximates the look of tables created via HTML. For an accurate view of a table, you must look at a document rendered by ReadTheDocs.

Note that a full (browsable) link to a location has the form: "http://cytoscape-working-copy.readthedocs.org/en/latest/Chapter_3_Launching_Cytoscape.html#mylink" where "http://cytoscape-working-copy.readthedocs.org/en/latest/" is the full URL, "Chapter_3_Launching_Cytoscape" is the root name of the file containing the target link, and "mylink" is a named section (e.g., <a name="mylink">System requirements</a>. A link between chapters in the document has the form [My Link](Chapter_3_Launching_Cytoscape.html#mylink), and a link within the same chapter has the form [My Link](#mylink).

## Rebuilding the Manual
The manual is automatically rebuilt by ReadTheDocs when the GitHub repository is updated. (This is courtesy of a WebHook that I installed per http://docs.readthedocs.org/en/latest/webhooks.html). 

The rebuild can be observed by logging into the ReadTheDocs account (see me for credentials) and choosing the "Cytoscape Working Copy" project. To see the build log, click on the grey Builds button. You can watch the progress of the build by manually refreshing your browser window until the build status shows either Passed or Failed. If it shows Passed, you can view the build result by clicking on the green View Docs button. 

Note that many errors (e.g., missing chapter files) fail silently. It's always best to verify recent changes by viewing them in the built document.

## Future Plan
The build process is adequate for development, but must be augmented once we reach a release stage. At that point, a released manual should be paired with a Cytoscape release, and should not be changed until the next Cytoscape release.

However, the Cytoscape development process entails continuous manual changes in anticipation of a future release. To reconcile this, I expect that we will create a separate ReadTheDocs project that keys off a GitHub branch (e.g., "development"), and that the branch will be merged into the master (and rebuilt) immediately before a new release. This arrangement has yet to be made. 

Note, too, that even development projects appear to be visible within ReadTheDocs and searchable via Google search. It's likely that having work-in-progress versions visible to general public search will cause confusion in the user community, and we need to investigate ways to avoid publishing in-progress versions.

## Process for Importation
The existing Cytoscape user manual was ported from Moin Moin to Markdown/ReadTheDocs according to a formula laid out by Kozo Nishida. The original port is contained in the "originals" directory and are not part of the current document build. For posterity, the initial instructions were:

1. Export http://wiki.cytoscape.org/Cytoscape_3/UserManual to a
docbook xml. (https://github.com/kozo2/cytoscape3-usermanual/blob/master/UserManual.xml)

2. Convert UserManual.xml to UserManual.md
(https://github.com/kozo2/cytoscape3-usermanual/blob/master/UserManual.md)
with ```pandoc -f docbook -t markdown -s UserManual.xml -o UserManual.md```

3. Separate UserManual.md per chapter manually.
(https://github.com/kozo2/cytoscape3-usermanual/tree/master/docs)

4. Find all pictures used by each chapter and put them into the Images directory. Resolve all picture references in the text by hand.

5. Build and deploy #4 with mkdocs and readthedocs.
 
Additionally:

1. Create a new project in ReadTheManual, and create a WebHook from GitHub to ReadTheDocs via http://docs.readthedocs.org/en/latest/webhooks.html

1. Note that text is processed by Sphinx, which is documented here: http://www.sphinx-doc.org/en/stable/contents.html
