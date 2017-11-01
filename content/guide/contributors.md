---
title: Contributors
type: page
---

## Adding Contributors to Your Project

### Where

Contributors can be listed in your `publication.yml` under `primary_contributor`, `secondary_contributor`, or `publication_team`; or in the YAML block at the top of any page in your project, under `contributor`.

`primary_contributor`s are authors, editors and others who would appear on a publication’s cover or title page. In Quire templates, they are typically used on the cover, the menu and in the [metadata embedded in your publication](metadata.md); listed as the creators of the publication.

`secondary_contributor`s are not typically shown in the menu or cover, but are often included in book metadata, and may also be referenced by the `q-contributor` shortcode as noted below. In future iterations of Quire, we hope to be able to reference contributors listed here from individual pages.

The `publication_team` are those that worked on the publication (editors, designers, developers, and the like), and can be listed using the `q-contributor` shortcode, often on an About or Copyright page. `publication_team` data is not otherwise inlcuded in publication metadata, or used in other Quire templates.

### How

Wherever they are listed, the following YAML attributes can be used for your contributors:

```YAML
- id:
  first_name:
  last_name:
  full_name:
  file_as:
  title:
  affiliation:
  role:
  role_code:
  pic:
  url:
  bio:
```

Not all of these are required. Depending on your usage, you may need as little as  `first_name` and `last_name`, or just `full_name`. See the [`q-contributor` shortcode reference](reference/shortcodes.html#q-contributor) for details on each of the standard contributor attributes.

### Alternatives

Contributors may also be listed in the `contributor_as_it_appears` field in your `publication.yml` file. This value will override the indivdual `primary_contributor`s listed on the cover, the menu and in the book metdatea. Useful when you want to include specific language about their role. For example: "Edited by Jane Smith and John Doe".

Contributors listed on the cover can be further refined with `cover_contributor` which can be used on any page with `type: cover` (typically your `index.md` file). Rather than a list of contributors, this field accepts a Markdown-formatted text string or block. In this way you could add italics, list formatting, or other structure or style to these contributors that’s not available elsewhere.



## Displaying a List of Contributors

The `q-contributor` shortcode can be used to create a page of contributor biographies, a section of bios for a single page, a list of contributors, a byline for a particular page, or other similar applications. The shortcode requires both a "range" and a "type" value.

Sample: `{{< q-contributors range="page" type="bio" >}}`

### range

The "range" value determines which contributors will be included in the list. Possible "range" values are:

- **page**: Only the contributors listed for the page the shortcode appears on.
- **essays**: Contributors on any page in your publications with `type: essay`.
- **all**: All contributors.
- **primary**: Contributors listed under `primary_contributor` in your `publication.yml` file.
- **secondary**: Contributors listed under `secondary_contributor` in your `publication.yml` file.
- **publication-team**:

### type

The "type" value determines what information will be listed for each contributor in the "range", and how it will be formatted. Possible "type" values are:

- **initials**: Looks for the capital letters in a contributor first and last name and concatenates them together. Jane Pauley, becomes J.P.; Ralph Waldo Emerson becomes R.W.E.
- **name**: Just the first and last name.
- **name-plus**: The first and last name with, when available, their title and affiliation on a line below.
- **bio**: First and last name, with pic, url, and bio as available. Plus a link to their contribution.

### Notes and Warnings

There are some limitations to the `q-contributor` shortcode.

This shortcode can be used multiple times on a page, but ONLY if the same range is referenced.

Users can use a `file_as` value to control sort order. Otherwise lists are sorted alphabetically by `last_name`. If you wanted, for example, a list of essay contributors ordered in the way they are ordered in the page YAML, you could assign a numeric `file_as` value to each. 1, 2, 3 etc. Note though that this `file_as` override will cary over to other uses of the shortcode. For example, a complete list of contributors at the end of a volume of collected papers.

If a contribuor is listed in many papers, the information in last listing will override all the others.

Contributors with the same exact name will override eachother. But using a `file_as` value would fix this, and that value wouldn't show up in the interface. For example if there are two Jane Smiths, assigning a `file_as` value of "Smith, Jane 1" to one and "Smith, Jane 2" will sort them in that order, but there names would still be listed as Jane Smith.

