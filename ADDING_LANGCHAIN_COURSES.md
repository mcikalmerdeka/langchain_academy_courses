# Adding LangChain Academy Courses - Guide

## 📚 Overview

This guide explains how to properly add LangChain Academy courses to your main repository without encountering nested git repository issues.

## ❌ The Problem: Nested Git Repositories

When you clone or pull LangChain Academy course repositories, they come with their own `.git` folders, creating **nested git repositories**. This causes issues when trying to add them to your main repository.

### Symptoms:
- `git add` fails with "pathspec did not match any files"
- Warning: "adding embedded git repository"
- Unable to track course files in your main repository
- Git treats the course folder as a single file instead of tracking individual files

### Why This Happens:
LangChain Academy courses are individual git repositories. When you clone/pull them into your main repository, git sees the nested `.git` folder and treats the entire course as a submodule reference rather than regular files.

## ✅ The Solution

### Step 1: Remove the Nested `.git` Folder

After cloning/pulling a course, remove its `.git` folder:

```powershell
# Windows PowerShell
Remove-Item -Recurse -Force course_folder_name\.git

# Or using Command Prompt
rmdir /s course_folder_name\.git

# Linux/Mac
rm -rf course_folder_name/.git
```

### Step 2: Add the Course Content

```bash
git add course_folder_name/
git commit -m "Add LangChain Academy [Course Name] course"
git push origin main
```

## 🔄 Complete Workflow for Adding New Courses

### Method 1: Clone and Clean (Recommended)

```bash
# 1. Clone the course repository
git clone https://github.com/langchain-ai/course-repo-name.git

# 2. Remove the nested .git folder
Remove-Item -Recurse -Force course-repo-name\.git

# 3. Rename if needed (optional)
mv course-repo-name/ descriptive-course-name/

# 4. Add to your main repository
git add descriptive-course-name/
git commit -m "Add LangChain Academy [Course Name] course"
git push origin main
```

### Method 2: Download and Extract

```bash
# 1. Download as ZIP from GitHub (no .git folder included)
# 2. Extract to your desired folder name
# 3. Add directly to your repository
git add new-course-folder/
git commit -m "Add LangChain Academy [Course Name] course"
git push origin main
```

## 📁 Recommended Repository Structure

```
Langchain Academy/
├── introduction_to_langgraph/          # ✅ Course 1
├── langchain_fundamentals/             # 🔄 Course 2
├── advanced_rag_techniques/            # 🔄 Course 3
├── multi_agent_systems/               # 🔄 Course 4
├── pyproject.toml                     # Main project config
├── uv.lock                            # Dependency lock file
├── README.md                          # Main repository documentation
├── ADDING_LANGCHAIN_COURSES.md        # This guide
└── .gitignore                         # Git ignore rules
```

## 🚨 Troubleshooting

### If You Already Added a Course with Nested .git

```bash
# 1. Remove from git tracking
git rm --cached course_folder_name

# 2. Remove the nested .git folder
Remove-Item -Recurse -Force course_folder_name\.git

# 3. Re-add the course
git add course_folder_name/
git commit -m "Fix: Re-add [Course Name] without nested git repository"
```

### If Git Shows "embedded git repository" Warning

This warning means you're trying to add a folder that contains a `.git` folder. Follow the solution steps above to remove the nested `.git` folder first.

## 📝 Best Practices

1. **Always remove `.git` folders** from cloned courses before adding to your main repository
2. **Use descriptive folder names** for courses (not just the original repository name)
3. **Keep course materials organized** in separate folders
4. **Document your learning progress** with meaningful commit messages
5. **Create branches** for experimenting with course code if needed

## 🔍 Verification

After adding a course, verify it was added correctly:

```bash
# Check that files are tracked (not just the folder)
git status

# Should show individual files, not just the folder name
# Good: "new file: course_name/module-1/notebook.ipynb"
# Bad: "new file: course_name" (this means nested .git wasn't removed)
```

## 📚 Course Sources

- [LangChain Academy](https://academy.langchain.com/)
- [LangChain Academy GitHub](https://github.com/langchain-ai/langchain-academy)

---

**Created:** $(Get-Date -Format "yyyy-MM-dd")  
**Last Updated:** $(Get-Date -Format "yyyy-MM-dd")  
**Purpose:** Reference guide for adding LangChain Academy courses without git conflicts 