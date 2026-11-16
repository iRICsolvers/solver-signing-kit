# iRIC solver signing kit

iRICsolvers のソルバーを配信するときに、`install/` の exe / dll に iRIC-UC の証明書でデジタル署名を付けるためのキットです。

A kit that signs the exe / dll files in `install/` with the iRIC-UC certificate when an iRICsolvers solver is released.

## ダウンロード / Download

最新版 / Latest: [solver-signing-kit.zip](https://github.com/iRICsolvers/solver-signing-kit/releases/latest/download/solver-signing-kit.zip)

```powershell
Invoke-WebRequest https://github.com/iRICsolvers/solver-signing-kit/releases/latest/download/solver-signing-kit.zip -OutFile solver-signing-kit.zip
Expand-Archive .\solver-signing-kit.zip -DestinationPath C:\path\to\your-solver -Force
```

## 使い方 / How to use

ソルバー開発者向けの案内を参照してください。 / See the guide for solver developers.

- 日本語: https://claude.ai/artifact/HHyWghf7mYd9LggX7mdGE1
- English: https://claude.ai/artifact/MRCVRRNbAQoC2dTRSzLAEs

## 対象 / Scope

- iRICsolvers 組織のリポジトリ（公開・非公開とも）の `main` / `master` ブランチからだけ署名できます。
  Signing works only from the `main` / `master` branch of repositories in the iRICsolvers organization (public or private).
- Python だけのソルバー（exe も dll もない）は対象外です。
  Python-only solvers (no exe or dll) are out of scope.

## このリポジトリの構成 / Layout

`kit/` の中身が zip の中身です。`kit/.github/workflows/build.yml` は、このリポジトリでは動きません（ソルバーのリポジトリに展開したときに動きます）。

The contents of `kit/` are what the zip contains. `kit/.github/workflows/build.yml` does not run in this repository; it runs after you extract it into a solver repository.

キットの仕組みの詳細は [kit/tools/release/README.md](kit/tools/release/README.md) を参照してください。

## リリースの作り方（管理者向け） / Making a release (administrators)

```powershell
powershell -ExecutionPolicy Bypass -File .\kit\tools\release\package-signing-kit.ps1 -OutputPath .\dist\solver-signing-kit.zip
gh release create vYYYY.MM.DD .\dist\solver-signing-kit.zip --title "solver-signing-kit vYYYY.MM.DD" --notes "..."
```
