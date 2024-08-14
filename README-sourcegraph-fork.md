# Sourcegraph fork of Lexical

We forked the Lexical editor to fix a few bugs in the Cody chat @-mention menu. See the commit messages on our fork.

## Publishing

To "publish" a new `@lexical/react` package for consumption in the [Cody repository](https://github.com/sourcegraph/cody):

In this repository, run:

```
npm install
npm run prepare-release
cd packages/lexical-react/npm
TARBALL="tar czfv lexical-react-sourcegraph-fork-$(git rev-parse --short HEAD).tgz"
tar czfv $TARBALL .
gsutil cp $TARBALL gs://sourcegraph-assets/npm/
rm $TARBALL
```

Then in the Cody repository, update the root package.json's `pnpm.overrides.@lexical/react` value to be `https://storage.googleapis.com/sourcegraph-assets/npm/$TARBALL`, where `$TARBALL` is the actual filename you just uploaded. Run `pnpm install`.

## Developing

To use the Lexical playground to develop, just run `npm run start` in this repository.

To use your local Lexical changes in Cody, the easiest way is to just import from this repository's sources directly. For example, instead of:

```typescript
import { LexicalTypeaheadMenuPlugin, type MenuOption } from '@lexical/react/LexicalTypeaheadMenuPlugin'
```

use:

```typescript
import {
    LexicalTypeaheadMenuPlugin,
    type MenuOption,
} from '/Users/USERNAME/src/github.com/facebook/lexical/packages/lexical-react/src/LexicalTypeaheadMenuPlugin.tsx'
```

(where the file path is the correct one on your machine).
