.. _changelog:

Changelog
=========

[unreleased]
------------

Added
.....

* Added search for profiles (`#163 <https://github.com/jaywink/socialhome/issues/163>`_)

  There is now a global search in the right side of the header. The search returns matches for local and remote profiles based on their name and username part of the handle. Profiles marked with visibility ``Self`` or ``Limited`` are excluded from the search results. Profiles marked with visibility ``Site`` will be excluded if not logged in, leaving only public profile results. If a direct match happens with a full handle, a redirect is done directly to the searched profile.

  **IMPORTANT for node maintainers**. After pulling in this change, you MUST run the command ``python manage.py rebuild_index`` to create the search index. Not doing this will cause an error to be raised when trying to search. The indexes are kept up to date automatically after running this command once.

* When searching for profiles based on handle, fetch profile from remote if it isn't found locally (`#163 <https://github.com/jaywink/socialhome/issues/163>`_)

Fixed
.....

* Make reply notifications to local users not send one single email with all local participants, but one email per participant. Previous implementation would have leaked emails of participants to other participants.
* Correctly send replies to remotes (`#210 <https://github.com/jaywink/socialhome/issues/210>`_)

  If parent content is local, send via the relayable forwarding mechanism. This ensures parent author signs the content. If parent author is remote, send just to the remote author. The remote author should then relay it.
* Ensure calling ``Profile.private_key`` or ``Profile.key`` don't crash if the profile doesn't have keys. Now the properties just return ``None``.
* Fix regression in profile all content stream load more functionality. (`#190 <https://github.com/jaywink/socialhome/issues/190>`_)
* Filter out "limited" visibility profiles from API list results. These profiles are not available in the search so they shouldn't be available to list through the API either.

0.1.0 (2017-07-27)
------------------

Initial versioned release. Main implemented features:

* Working streams (followed, public, profiles)
* Content creation
* Content OEmbed / OpenGraph previews
* Replies
* Follow/unfollow of profiles
* Contacts list
* Pinning content to profile