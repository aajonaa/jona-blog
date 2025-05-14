# jona-blog
I want to create a blog of mine which records how I solve the problem in hand. The backbone is hugo with the theme hugo-PaperMod.

---

## My Setup Notes

### Dev and Production settings
- Dev: nginx listen 443, hugo bind 127.0.0.1, port 1234, http://sag.ubu:443/, appendPort=false
- Production: nginx listen 80, hugo bind 127.0.0.1, port 1313, http://sag.ubu/, appendPort=false

### Bashrc alias
- alias hugodev='hugo server -D --port=1234 --bind="127.0.0.1" --baseURL="http://sag.ubu:443/" --appendPort=false'

### Bash script of how to use the command hugoPost 'title'
hugoPost() {
  if [ -z "$1" ]; then
    echo -n "Please provide a post title."
    return 1
  fi

  TITLE="$1"  # The original title as input by the user
  SLUG="$TITLE"

  BUNDLE_PATH="content/posts/$SLUG"
  mkdir -p "$BUNDLE_PATH"
  mkdir -p "$BUNDLE_PATH/images"

  # Create the index.md file using Hugo.
  hugo new --kind post "posts/$SLUG/index.md"

  echo "Created post bundle at $BUNDLE_PATH"
  echo "Edit your content in $BUNDLE_PATH/index.md"
}
