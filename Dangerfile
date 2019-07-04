# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if gitlab.mr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Warn when there is nobody assigned to this merge request
warn "This MR does not have any assignees yet." unless gitlab.mr_json["assignee"]

# Fail when there is no description of the merge request
failure "Please provide a summary in the Merge Request description" if gitlab.mr_body.length < 5

if git.modified_files.include? "Podfile"
    warn "Please put all of the Podfile dependencies into your target branch, install them on that branch, and rebase your branch on top of it."
end
