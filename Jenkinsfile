// SPDX-FileCopyrightText: 2023 Zextras <https://www.zextras.com>
//
// SPDX-License-Identifier: AGPL-3.0-only

library(
    identifier: 'jenkins-lib-common@v4.10.3',
    retriever: modernSCM([
        $class: 'GitSCMSource',
        credentialsId: 'jenkins-integration-with-github-account',
        remote: 'git@github.com:zextras/jenkins-lib-common.git',
    ])
)

dt3_pipeline(
    repoName: 'carbonio-preview-db',
    packaging: [
        pkgbuildPath: 'package/PKGBUILD',
        buildFlags: '-ds',
        ubuntuSinglePkg: false,
        rockySinglePkg: false,
    ],
    docker: [[
        dockerfile: 'docker/preview-db-sidecar/Dockerfile',
        imageName: 'carbonio-preview-db-sidecar',
        platforms: ['linux/amd64', 'linux/arm64'] as Set,
        title: 'Carbonio Preview DB Sidecar',
        description: 'Carbonio Preview DB sidecar service',
    ]],
    reuse: [projectType: 'CE']
)
