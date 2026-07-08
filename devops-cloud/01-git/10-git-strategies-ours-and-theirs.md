## Question  
What are `ours` and `theirs` strategies in Git merges? How and when are they used?

###  Short Explanation  
This question checks whether you understand how to control merge behavior during conflicts — especially in tricky cases like rollbacks, overrides, or integration branches.

##  Answer  
- **`ours`** strategy favors **your current branch’s changes**, even if the other branch has different content.
- **`theirs`** isn't directly available as a merge strategy but can be used during conflict resolution in a rebase or a manual merge to **accept incoming changes over yours**.

###  Detailed Explanation  

####  `ours` Strategy (as a Git merge strategy)
When running a merge, you can tell Git:
> “Even though we’re merging, if there’s a conflict — pick my current branch’s version.”

Used like this:
```bash
git merge -s ours feature-branch
```

 **Important:** This does *not* mean it merges and keeps both sets of changes. It **pretends to merge** but **keeps only your current branch's content**, marking the merge as done.

 **Use cases:**
- When rolling back a hotfix and keeping current stable state
- When merging a long-dead branch just to close it but keep your branch's state intact

---

####  `theirs` Strategy (used manually during conflicts)
There is **no `-s theirs` strategy** at the command line merge level.

However, when resolving a conflict manually, you can choose the **incoming branch's changes** using:
```bash
git checkout --theirs conflicted_file.txt
git add conflicted_file.txt
```

This tells Git:
> “For this conflicted file, discard my local version and use the version from the branch I’m merging in.”

 **Use cases:**
- When the incoming changes are definitely correct
- During `git rebase` when resolving repetitive or well-understood conflicts

---

###  Summary Table

| Strategy  | Behavior                                      | Use When...                                             |
|-----------|-----------------------------------------------|----------------------------------------------------------|
| `ours`    | Keeps **current branch’s** content             | You want to keep your version, discard the incoming one |
| `theirs`  | Keeps **incoming branch’s** content            | You want to override with the other branch’s changes    |

---