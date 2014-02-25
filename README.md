This is work-in-progress.

A basic syncronization utility for [vdir](https://github.com/untitaker/vdir). Should be able to sync both CardDAV and CalDAV in the end.

## A little bit about the code architecture

There are storage classes which control the access to one vdir-collection and
offer basic CRUD-ish methods for modifying those collections. The exact
interface is described in `vdirsyncer.storage.base`, the `Storage` class should
be a superclass of all storage classes.

One function in `vdirsyncer.sync` can then be called on two instances of
`Storage` to syncronize them, due to the abstract API storage classes are
implementing, the two given instances don't have to be of the same exact type.
This allows us not only to syncronize a local vdir with a CalDAV server, but
also syncronize two CalDAV servers or two local vdirs.

## Rough list of things that need to be done
  - implement CalDAVStorage and CardDAVStorage

    ~~While events generally have to be referenced by href, there's an example in
    the [CalDAV RFC](http://www.ietf.org/rfc/rfc4791.txt) (Ctrl+F for "by UID")
    on how to get events by UID. In the worst case we have to find out the href
    through that every time we want to delete or update an event.~~
    *hopefully this is no longer a real concern due to the rewrite of the storage
    API with commit `4b92442`. Probably it's just going to be copy-and-paste from 
    [khal](https://github.com/geier/khal/blob/master/khal/caldav.py#L99).*

  - finish the CLI and decide on a config format
  - moar tests
  - conflict resolution
  - Everywhere you find TODO in the sourcecode
