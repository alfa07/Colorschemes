# Colorschemes — contributor notes

## Development setup

This repo uses Python (see `requirements.txt`) to generate colorschemes from
templates. Install the dependencies once, ideally in a virtualenv:

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

Then generate schemes with `./generate_colorscheme.sh` (or run `ez.py`
directly).

## Git hooks

This repo ships commit hooks in `.githooks/` that enforce the commit identity
and block `Co-Authored-By:` trailers. Git does not run tracked hooks on clone
(that would be a security hole), so enable them once per clone:

```bash
git config --local core.hooksPath .githooks
```

Once enabled:

- **`pre-commit`** rejects the commit unless the author *and* committer email
  are `maximsok@gmail.com`. On mismatch it prints the fix:
  `git config --local user.name "Maxim Sokolov" && git config --local user.email "maximsok@gmail.com"`.
- **`commit-msg`** rejects any message containing a `Co-Authored-By:` trailer.

The hooks are repo-local on purpose — a global hook would break commits made
under other identities (e.g. work repos).
