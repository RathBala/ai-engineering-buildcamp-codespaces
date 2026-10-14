# ai-engineering-buildcamp-codespaces
Everything I'm working on in relation to this course

## Course environment

Open the existing GitHub Codespace and use its terminal in `/workspaces/ai-engineering-buildcamp-codespaces`. This project uses Python 3.14 and uv.

Run `uv sync --locked` to restore dependencies. Keep `pyproject.toml`, `uv.lock` and `.python-version` together. Git ignores the .venv environment and secret files.

Open `setup.ipynb`, select `.venv/bin/python` as its Python environment, and choose Run All. It checks the environment, creates the OpenAI client and verifies authentication with a read-only models request. It prints only safe pass/fail messages.

The repository Codespaces secret `OPENAI_API_KEY` must be set before starting the Codespace. Restart after changing the secret. No separate sign-in is needed inside the notebook. Never paste the key into code or notebook output.

For a repeatable check from the project directory:

```bash
timeout 90s uv run jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=60 setup.ipynb
```

Alternatively, run `uv run jupyter notebook` and open the private forwarded port. Use the token shown in your own terminal, without sharing it.

Stop the Codespace when finished. Files and the installed environment survive stopping. Commit and push source files separately when ready to preserve them in GitHub.

## Check output and API access

| Surface | Trigger and destination | Data and purpose | Retention and checks |
| --- | --- | --- | --- |
| Notebook checks in `setup.ipynb` | Run All or the documented nbconvert command; output is saved in the notebook | Fixed success messages and sanitized HTTP status codes explain setup failures. No keys, prompts, account IDs or model lists are printed. | Outputs remain until rerun or cleared. Notebook validation and the source secret scan guard the saved artifact. The repository owner controls it. |
| OpenAI authentication | The notebook authentication cell calls `api.openai.com/v1/models` through the official SDK | The existing course key authenticates the read-only request. No user content is sent and no model generation runs. | Provider retention settings were not audited. The successful request verifies authentication; it does not verify a particular model's generation permissions. |

No product analytics or third-party tracking is added.
