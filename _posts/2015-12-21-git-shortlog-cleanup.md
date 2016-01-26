---
layout: post
title: git cleanup
---

Going through git repos that I'm still using and making them all use a consistent user name and email so the commits link by to my profile.
The anonymous noreply email didn't work.

Having to filter-branch everything so any other machines with these projects need to pull them before pushing and clobbering the rewritten usernames.

  git filter-branch --commit-filter \
  'if [ "$GIT_AUTHOR_NAME" = "lucasw" ]; then \
  export GIT_AUTHOR_NAME="Lucas Walter";\
  export GIT_AUTHOR_EMAIL=lucasw@example.com;\
  export GIT_COMMITTER_NAME="Lucas Walter";\
  export GIT_COMMITTER_EMAIL=lucasw@example.com;\
  fi;\
  git commit-tree "$@"'
