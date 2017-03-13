# Pod

## Create Pod

```
pod lib create <lib_name>
```

## Update Pod

1. Add cardinalblue pod repo `pod repo add cb git@github.com:cardinalblue/CocoaPodsSpecs.git` (Only first time, `cb` is the name of the repository, you can name it anything)
2. Update `s.version` in `XXX.podspec`
3. Add tag
`git tag <version> && git push origin <version>`
4. Push podspec `pod repo push cb --allow-warnings --use-libraries`
