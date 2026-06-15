[update-readmes]   Mode: rewrite — migrating to template structure...
# confmgr

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/confmgr)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/confmgr.git
cd confmgr
```

## Usage


**Javascript**

        const ConfigManager = require('confmgr').ConfigManager;

**Typescript**

        import { ConfigManager } from 'confmgr';

### Some details

You may have a look at the samples in the `samples` folder. There are simple demos in Typescript and Javascript.

In short, you first need to define the specs of your config. You can do that using Yaml or using a Factory directly, as shown below:

**Using a Yaml file**

This is the commend option and likely the easiest one.

    TS_SAMPLE:
      MODULE_01:
        PARAM1:
          description: some param1
        PARAM2:
          description: some param2
        SECRET:
          description: some secret
          masked: true
        BOOL1:
          description: bool1
          type: boolean
          default: true
        BOOL2:
          description: bool2
          type: boolean
          default: true
        ARRAY1:
          description: some array
          default: [1, 'a', true, { foo: bar }]
        OBJ1:
          description: some object
          default: { foo: bar, list: [1, 2, 3] }

      MODULE_02:
        REGEXP:
          description: some regexp
          regexp: ^\d{2}_\d{2}
        MANDAT_WITH_DEF:
          description: some optional param
          mandatory: true
          default: 42
        MANDAT_NO_DEF:
          description: some optional param
          mandatory: true

**Using the Factory**

    import { SpecsFactory } from 'confmgr'

    const prefix = 'TS_SAMPLE'
    const mod = 'MODULE_01'

    const factory = new SpecsFactory({ prefix })
    factory.appendSpec(mod, factory.getSpec('PARAM1', 'some param1'))
    factory.appendSpec(mod, factory.getSpec('PARAM2', 'some param2'))
    factory.appendSpec(
        mod,
        factory.getSpec('SECRET', 'some secret', { masked: true })
    )
    factory.appendSpec(
        mod,
        factory.getSpec('REGEXP', 'some regexp', { regexp: /^\d{2}_\d{2}/ })
    )
    factory.appendSpec(
        mod,
        factory.getSpec('MANDAT1', 'some mandatory param', { mandatory: true })
    )
    const specs = factory.getSpecs()

    export default specs

Once you defined the specs for your config, you need to create an `.env` file (unless you plan on passing the config as Environment Variables). It looks as following for the specs mentioned above:

    TS_SAMPLE_MODULE_01_PARAM1=12
    TS_SAMPLE_MODULE_01_PARAM2=44
    TS_SAMPLE_MODULE_01_SECRET=secret
    TS_SAMPLE_MODULE_01_REGEXP=68_77
    TS_SAMPLE_MODULE_01_MANDAT1=27

You may now use your config:

    import { ConfigManager } from 'confmgr'
    import mySpecs from './configSpecs'

    const config = ConfigManager.getInstance(mySpecs).getConfig()
    const valid = config.Validate()
    console.log(`Your config is${valid ? '' : ' NOT'} valid!`)

    config.Print({ color: true, compact: false })

    console.log(`PARAM1=${config.Get('MODULE_01', 'PARAM1')}`)

You should never display your config, especially in your logs, as it may contain some secrets! Instead, use the Print() method of the ConfigManager, it will mask sensible data.

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/confmgr`](https://github.com/Interested-Deving-1896/confmgr) and mirrored through:

```
Interested-Deving-1896/confmgr  ──►  OpenOS-Project-OSP/confmgr  ──►  OpenOS-Project-Ecosystem-OOC/confmgr
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[MIT](https://github.com/Interested-Deving-1896/confmgr/blob/master/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
