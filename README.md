# XOD Enhancement Notes

This repository contains a collection of documents called XENs aid to developing [XOD](https://github.com/xodio/xod) visual programming language and IDE.

One XEN is a Markdown document describing a single feature, library, or adjustment bigger than trivial. XENs pass through the usual coding pipeline which involves pull requests and reviews. This way the proposals tend to be analyzed in more detail, significantly changed, or just rejected before they hit the development backlog.

The idea of XENs is borrowed from [Python PEPs](https://github.com/python/peps) and RFC processes of other projects.

## Naming

Each XEN lives in its directory named like XEN-Y999 where `Y` is a letter-encoding its topic and 999 is a unique number within this topic. The letter code is as follows:

| Letter | Topic
| ------ | -----
| F      | A core language feature or concept
| L      | Changes or improvements to the standard library
| R      | C++ runtime or generated code enhancements

## Front matter

A XEN may include additional metadata at the beginning of the document with the following fields:

`status`. One of `draft` (the default status), `scheduled` (an issue to implement the XEN is put on the backlog or implementing right now, edit with care), `closed` (already done or rejected, the XEN if frozen).

`issue`. A direct link to the GitHub issue proposing to implement the XEN.

`champion`. A direct link to XOD user profile who authored the XEN or the current lobbyist.

## Contributing

You can suggest a change to the existing XEN. Change it and open a new pull request. If not sure, all XENs are also discussed on the [XOD forum](https://forum.xod.io/c/xens).

Anyone can PR a new XEN. Make sure to read [contributing guidelines](./CONTRIBUTING.md) and craft a detailed document like those already in the repo.
