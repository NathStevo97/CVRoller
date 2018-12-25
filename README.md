CVRoller
=========

This is a script designed to be a generic automatic document compiling language, with an eye on catering to the creation of CVs.

The goal is to have a format for writing document layout structures and data (including from spreadsheet, JSON, .bib, or sites like ORCID or PubMed), then reading in both and spitting out any number of varieties of CV (including website, PDF, and Word).

This project is under construction. Soon it will be to the point where it's basically usable (at least on the base level), but without implementation of some features that may come in handy, and which requires learning the layout language to use. Eventually the goal is to have a system that's easy to use without having to learn too much.

For an explanation of how the CV layout language works, see LayoutInstructions.md. For an explanation on how to put together the CV data file, see SpreadsheetInstructions.md.

Near Term Fixes and Features
============================

Makin' Progress! Fixes/Features Added Since First Commit
----------------------------------
* Allow layout file to have two different versions of the same-named section
* Currently, if ID is missing in data, it's filled in with 1 to length. That's fine. But how to handle if only SOME ids are missing? <- will remain in original order
* Improve method for reading in options and layout structure
* From first-pass code turn important features into callable functions for later flexibility
* Allow structure file to have comments; omit lines starting with comment character(s?) and update Layout Instructions to match
* Allow sections to have their own data-in files (especially .bib for citations), then append that data to the main data already read in before processing.
* Allow data to be read in from JSON or other format rather than spreadsheet
* Add CSV import
* Allow commas in version options
* Import citations from .bib or JSON, format them, order them, display them.
* Turn 'meat' construction into callable functions for flexibility.

Small Fixes/Features to Come
--------------------
* Currently has heavy reliance on layout file ending lines with \n. Be more flexible
* Add LaTeX-out and Word-out
* Put in way of locating layout file other than the placeholder hardcoding.
* Figure out way to allow tables more easily (tables currently work but you have to very oddly stick the table header row in the format option). Note this follows from the markdown package's markdown parser requiring a table header.
* Find all HTML tags in citation formatting and change back to Markdown for the purpose of eventual LaTeX-out and Word-out. <i> and <b> already changed back. But are there others?
* JSON citation input is untested
* Suppress citeproc-py warnings for unsupported fields when reading in bibtex files

Big Fixes/Features to Come
------------------
* Allow theming! Native themes specific to CVRoller (this actually would be a small fix), or, ideally, working with other CV themes like markdown-cv http://elipapa.github.io/markdown-cv/ or LaTeX moderncv https://www.ctan.org/pkg/moderncv. Add theme option to versions.

Medium/Far Term Fixes and Features to Come
----------------------------------
* Import citations from online databases like ORCID and PubMed
* Add scheduler so that if run on a server, will regularly check for updates to data and re-generate files
* Add uploader or FTP so that the generated CVs can be automatically uploaded to a website
* Program/website that makes it easy to generate layout files so people don't have to learn the language
* Program/website that makes it easy to generate CV data file
* Program/website that lets you make an account and just put all the info on there so it can run

Original Planned Additions Perhaps Abandoned or Not a Problem
----------------------------------
* Allow other spreadsheet formats <- maybe not necessary, allows CSV, Excel, JSON already
* Current implementation uses pandas to read in data as strings, which turns missings into the actual string 'nan'. Is that the best way?
* Is there a better way of getting line breaks from the layout and data files than forcing people to write \br and turning it into space-space-\n?
* Figure out how to import and use CSL files without having to write them to disk