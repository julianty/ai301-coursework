### Environment

- OS: Windows 11, running commands in Git Bash
- Python: 3.11.8 (python.org installer)
- pytest: 9.1.1
- Code: upstream `main` at commit `f89c06f` (2026-09-16), no local changes

### Setup

From a fresh clone of the repo:

```bash
PATH="/path/to/python311:$PATH" make setup
```

Note: in my Git Bash, `python` pointed to an MSYS2 Python, which creates
`.venv/bin/` instead of `.venv/Scripts/`, so `make setup` failed. Putting the
python.org Python first on PATH fixed it.

### Steps and observed output

Run the test with `--runxfail`, so pytest ignores the `xfail` marker and reports the real failure:

```text
$ .venv/Scripts/python -m pytest "tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy" -v --runxfail
```

Local paths replaced with <repo>, and plugin header lines trimmed to [...]; otherwise unedited.

```
============================= test session starts =============================
platform win32 -- Python 3.11.8, pytest-9.1.1, pluggy-1.6.0 -- <repo>\.venv\Scripts\python.exe
rootdir: <repo>
configfile: pyproject.toml
[...]
collecting ... collected 1 item

tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy FAILED [100%]

================================== FAILURES ===================================
_______________ TestReadmeParser.test_extract_heading_hierarchy _______________

self = <tests.unit.test_readme_parser.TestReadmeParser object at 0x00000249F6EDEE90>
parser = <ingestion.parsers.readme_parser.ReadmeParser object at 0x00000249F6EFDA10>

    @pytest.mark.xfail(
        strict=True,
        reason="issue #71 (manifest H-04): heading hierarchy fixture is indented, so it has no headings",
    )
    def test_extract_heading_hierarchy(self, parser):
        """Test heading hierarchy extraction."""
        markdown = """
        # Main Title
        Some content

        ## Subsection
        More content

        ### Sub-subsection
        Even more content

        ## Another Section
        Final content
        """
        headings = parser._extract_heading_hierarchy(markdown)

        assert isinstance(headings, list)
>       assert len(headings) > 0
E       assert 0 > 0
E        +  where 0 = len([])

tests\unit\test_readme_parser.py:156: AssertionError
=========================== short test summary info ===========================
FAILED tests/unit/test_readme_parser.py::TestReadmeParser::test_extract_heading_hierarchy
============================== 1 failed in 0.19s ==============================
```
