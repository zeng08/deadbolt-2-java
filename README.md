deadbolt-2-java
===============

[![Maven Central](https://img.shields.io/badge/Sonatype%20snapshots-2.5.0--SNAPSHOT-brightgreen.svg)](https://oss.sonatype.org/content/repositories/snapshots/be/objectify/deadbolt-java_2.11/2.5.0-SNAPSHOT/) [![Build Status](https://travis-ci.org/schaloner/deadbolt-2-java.svg?branch=master)](https://travis-ci.org/schaloner/deadbolt-2-java) [![Join the chat at https://gitter.im/schaloner/deadbolt-2](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/schaloner/deadbolt-2?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


Idiomatic Java API for Deadbolt 2, an authorisation module for Play 2.

Jump straight in with the [quick start](./QuickStart.md)

Deadbolt 2 comprises of several modules - a common core, and language-specific implementations for Java and Scala.  Example applications and a user guide are also available.  

All modules related to Deadbolt 2, including the user guide, are grouped together in the [Deadbolt 2](https://github.com/schaloner/deadbolt-2) Github super-module.  Installation information, including Deadbolt/Play compatibility, can also be found here.

2.4.0 Release notes
-------------------

This list is incomplete!

- DeadboltPlugin has been removed - delete its entry in play.plugins
- F.Promise<> is now used by `DeadboltHandler` and `DynamicResourceHandler`.
- Don't return `null` where an `F.Promise` or `Optional` is required!

Finally, enable the DeadboltModule in application.conf

    play {
      modules {
        enabled += "be.objectify.deadbolt.java.DeadboltModule"
      }
    }


2.3.3 Release notes
-------------------

The primary focus of 2.3.3 was to move to a non-blocking architecture.  A simplification of structure was also needed, so a change to the DeadboltHandler interface in release 2.3.2 has been backed out; sorry about that.  Semantic versioning will continue shortly.

So, practical changes.

- DeadboltHandler#getSubject returns a Subject in place of an F.Promise<Subject>.  Where the subject is needed, the internal code will take care of wrapping the call in a Promise.
- There are no more timeouts, so deadbolt.before-auth-check-timeout and deadbolt.get-subject-timeout are no longer needed.  If they're defined in your config, they'll be ignored.

**What kind of idiot makes API-level changes in a patch release?**

Me, I'm afraid.  This will probably be the last release of Deadbolt for Play 2.3 and I want to keep the major and minor version of Deadbolt locked into the Play versions.  The change in 2.3.2 was, overall, ill-considered and shouldn't have happened so I'm looking at this as a bug fix more than a change.
