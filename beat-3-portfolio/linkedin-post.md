This fall I opened a pull request to MFC, a large open source scientific software project that simulates fluid flow. I renamed 11 outdated variable names in its testing code to match the project's style, and showed that all 776 of its test cases stayed exactly the same.

A change like this is small, but it touches code every test depends on, so the real work was proving I hadn't broken anything. I couldn't run the full test suite on my laptop, so I compared every test case before and after my change, and they matched exactly.

I also built a tool that helps me pick good first issues to work on. Its first run approved projects that were only a few weeks old, so I added a rule that fixes that, and now I check whether an issue has already been fixed before I claim it.

Today the pull request passes all of the project's automated checks and is waiting for a maintainer to review it. I also learned something about how this project works: I had marked the PR as ready to merge too early, and a maintainer asked me to leave it as a draft until they review it. I now read a project's review norms before I change anything on my pull request.

https://github.com/MFlowCode/MFC/pull/2131

#OpenSource #Python #SoftwareEngineering
