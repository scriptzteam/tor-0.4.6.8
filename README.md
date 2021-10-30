# tor-0.4.6.8
```
Changes in version 0.4.6.8 - 2021-10-26
  This version fixes several bugs from earlier versions of Tor. One
  highlight is a fix on how we track DNS timeouts to report general
  relay overload.

  o Major bugfixes (relay, overload state):
    - Relays report the general overload state for DNS timeout errors
      only if X% of all DNS queries over Y seconds are errors. Before
      that, it only took 1 timeout to report the overload state which
      was just too low of a threshold. The X and Y values are 1% and 10
      minutes respectively but they are also controlled by consensus
      parameters. Fixes bug 40491; bugfix on 0.4.6.1-alpha.

  o Minor features (fallbackdir):
    - Regenerate fallback directories for October 2021. Closes
      ticket 40493.

  o Minor features (testing):
    - On a testing network, relays can now use the
      TestingMinTimeToReportBandwidth option to change the smallest
      amount of time over which they're willing to report their observed
      maximum bandwidth. Previously, this was fixed at 1 day. For
      safety, values under 2 hours are only supported on testing
      networks. Part of a fix for ticket 40337.
    - Relays on testing networks no longer rate-limit how frequently
      they are willing to report new bandwidth measurements. Part of a
      fix for ticket 40337.
    - Relays on testing networks now report their observed bandwidths
      immediately from startup. Previously, they waited until they had
      been running for a full day. Closes ticket 40337.

  o Minor bugfix (onion service):
    - Do not flag an HSDir as non-running in case the descriptor upload
      or fetch fails. An onion service closes pending directory
      connections before uploading a new descriptor which can thus lead
      to wrongly flagging many relays and thus affecting circuit building
      path selection. Fixes bug 40434; bugfix on 0.2.0.13-alpha.
    - Improve logging when a bad HS version is given. Fixes bug 40476;
      bugfix on 0.4.6.1-alpha.

  o Minor bugfix (CI, onion service):
    - Exclude onion service version 2 Stem tests in our CI. Fixes bug 40500;
      bugfix on 0.3.2.1-alpha.

  o Minor bugfixes (compatibility):
    - Fix compatibility with the most recent Libevent versions, which no
      longer have an evdns_set_random_bytes() function. Because this
      function has been a no-op since Libevent 2.0.4-alpha, it is safe
      for us to just stop calling it. Fixes bug 40371; bugfix
      on 0.2.1.7-alpha.

  o Minor bugfixes (onion service, TROVE-2021-008):
    - Only log v2 access attempts once total, in order to not pollute
      the logs with warnings and to avoid recording the times on disk
      when v2 access was attempted. Note that the onion address was
      _never_ logged. This counts as a Low-severity security issue.
      Fixes bug 40474; bugfix on 0.4.5.8.
```
