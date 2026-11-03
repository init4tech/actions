# image-scan.yml

## Base Usage

```yml
image-scan:
  uses: init4tech/actions/.github/workflows/image-scan.yml@<commit sha>
  with:
    list-command: grep -v -e '^#' -e '^$' .github/pinned-images.txt
```

Scans container images with [osv-scanner](https://github.com/google/osv-scanner).
The calling repository says which images through `list-command`, a shell
command run at its root that prints one image reference per line. Pin each
reference by digest, so the scan covers the image that runs.

On a pull request the job runs `list-command` at the base too, and scans only
the references the PR adds: the images it asks the repository to start using.
Every other run scans every reference.

It uploads a dependency report and never fails on a finding. The report holds:

- `summary.txt`: one line per image and package, `image<TAB>package<TAB>ids`,
  sorted. The ids are those of the package's vulnerabilities at or above
  `min-severity` that a fixed version of the package resolves; a package with
  none has no line. An image that could not be pulled has the line
  `image<TAB>-<TAB>unpullable`.
- One osv-scanner JSON report per image, with every finding.

A line per image and package is one thing a person can act on: rebuild or
re-pin the image so the package is at its fixed version. A vulnerability with
no fixed version is left to the per-image report, since nothing can be
updated for it yet.

Each image is pulled for the runner's platform, or failing that for arm64 or
amd64, so one list can hold images built for one architecture only. The scan
reads the image's layers and runs nothing. An image osv-scanner reads no
packages from, such as a static busybox, has no report and shows as "no
packages read" in the step summary. A scanner error on any image fails the
job.

## Required Parameters

### `list-command`

**Description:** The shell command that prints one image reference per line.

**Type**: `string`

## Optional Parameters

### `runs-on`

**Description:** The runner, as JSON: a label string, or an object for a runner group.

**Type**: `string`

**Default Value:** `'"ubuntu-latest"'`

### `artifact-name`

**Description:** The name of the uploaded report. Give each call its own name
when a workflow scans several lists.

**Type**: `string`

**Default Value:** `dependency-report-images`

### `min-severity`

**Description:** The lowest CVSS score a vulnerability group needs to appear in
`summary.txt`. The per-image reports keep every finding.

**Type**: `string`

**Default Value:** `7.0`

### `fixed-only`

**Description:** Keep in `summary.txt` only the vulnerabilities a fixed
version of their package resolves. Set it to `false` to list every
vulnerability at or above `min-severity`.

**Type**: `boolean`

**Default Value:** `true`

### `osv-scanner-version`

**Description:** The osv-scanner version to install, checked against
`taiki-e/install-action`'s manifest.

**Type**: `string`

**Default Value:** `2.7.0`

### `timeout-minutes`

**Type**: `number`

**Default Value:** `60`

## Secrets

### `dockerhub-username` and `dockerhub-token`

Optional. With both set, images are pulled as that Docker Hub user, under its
rate limit instead of the anonymous one. Use a read-only access token.

## Permissions Required

- `contents: read`
