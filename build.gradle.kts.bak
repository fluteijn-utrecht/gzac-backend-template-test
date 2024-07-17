@file:Suppress("UNCHECKED_CAST")

import org.jetbrains.kotlin.gradle.tasks.KotlinCompile

plugins {
    war
    // Idea
    idea
    id("org.jetbrains.gradle.plugin.idea-ext")

    // Spring
    id("org.springframework.boot")
    id("io.spring.dependency-management")

    // Kotlin
    kotlin("jvm")
    kotlin("plugin.spring")
    kotlin("plugin.jpa")
    kotlin("plugin.allopen")

    // Checkstyle
    id("org.jlleitschuh.gradle.ktlint")
    id("com.diffplug.spotless")
}

java.sourceCompatibility = JavaVersion.VERSION_17
java.targetCompatibility = JavaVersion.VERSION_17

repositories {
    mavenCentral()
    maven { url = uri("https://s01.oss.sonatype.org/content/repositories/snapshots/") }
    maven { url = uri("https://repo.ritense.com/repository/maven-public/") }
    maven { url = uri("https://repo.ritense.com/repository/maven-snapshot/") }
}

val valtimoVersion: String by project

dependencies {
    implementation(platform("com.ritense.valtimo:valtimo-dependency-versions:$valtimoVersion"))

//    implementation("org.springframework.boot:spring-boot-starter-data-jpa")
    implementation("com.ritense.valtimo:valtimo-dependencies")

//    implementation("com.ritense.valtimo:audit:$valtimoVersion")
//    implementation("com.ritense.valtimo:authorization:$valtimoVersion")
//    implementation("com.ritense.valtimo:besluit:$valtimoVersion")
//    implementation("com.ritense.valtimo:case:$valtimoVersion")
//    implementation("com.ritense.valtimo:connector:$valtimoVersion")
//    implementation("com.ritense.valtimo:contactmoment:$valtimoVersion")
//    implementation("com.ritense.valtimo:contract:$valtimoVersion")
//    implementation("com.ritense.valtimo:core:$valtimoVersion")
//    implementation("com.ritense.valtimo:dashboard:$valtimoVersion")
//    implementation("com.ritense.valtimo:document:$valtimoVersion")
//    implementation("com.ritense.valtimo:documenten-api:$valtimoVersion")
//    implementation("com.ritense.valtimo:form:$valtimoVersion")
//    implementation("com.ritense.valtimo:form-link:$valtimoVersion")
//    implementation("com.ritense.valtimo:form-flow:$valtimoVersion")
//    implementation("com.ritense.valtimo:form-flow-valtimo:$valtimoVersion")
//    implementation("com.ritense.valtimo:haalcentraal-brp:$valtimoVersion")
//    implementation("com.ritense.valtimo:keycloak-iam:$valtimoVersion")
//    implementation("com.ritense.valtimo:klant:$valtimoVersion")
//    implementation("com.ritense.valtimo:notes:$valtimoVersion")
//    implementation("com.ritense.valtimo:objects-api:$valtimoVersion")
//    implementation("com.ritense.valtimo:plugin-valtimo:$valtimoVersion")
//    implementation("com.ritense.valtimo:process-document:$valtimoVersion")
//    implementation("com.ritense.valtimo:smartdocuments:$valtimoVersion")
//    implementation("com.ritense.valtimo:web:$valtimoVersion")
//    implementation("com.ritense.valtimo:test-utils-common:$valtimoVersion")
    implementation("com.ritense.valtimo:local-document-generation")
    implementation("com.ritense.valtimo:local-resource")
    implementation("com.ritense.valtimo:local-mail")
    implementation("com.ritense.valtimo:milestones")
    implementation("com.ritense.valtimo:object-management")
    implementation("com.ritense.valtimo:objecten-api-authentication")
    implementation("com.ritense.valtimo:objecten-api")
    implementation("com.ritense.valtimo:objecttypen-api")
    implementation("com.ritense.valtimo:openzaak")
    implementation("com.ritense.valtimo:zaken-api")

//    implementation("mysql:mysql-connector-java")
    implementation("org.postgresql:postgresql:42.7.3")

    if (System.getProperty("os.arch") == "aarch64") {
        runtimeOnly("io.netty:netty-resolver-dns-native-macos:4.1.105.Final:osx-aarch_64")
    }

    // Kotlin logger
    implementation("io.github.microutils:kotlin-logging")

    // Testing
    testImplementation("com.ritense.valtimo:test-utils-common")
    testImplementation("org.springframework.boot:spring-boot-starter-test")
    testImplementation("org.camunda.bpm.assert:camunda-bpm-assert:15.0.0")
    testImplementation("org.camunda.bpm.extension:camunda-bpm-junit5:1.1.0")
    testImplementation("org.camunda.bpm.extension:camunda-bpm-assert:1.2")
    testImplementation("org.camunda.bpm.extension:camunda-bpm-assert-scenario:1.1.1")
    testImplementation("org.camunda.bpm.extension.mockito:camunda-bpm-mockito:5.16.0")
    testImplementation("org.mockito:mockito-core:4.4.0")
    testImplementation("org.mockito.kotlin:mockito-kotlin:4.0.0")
}

tasks.withType<KotlinCompile> {
    kotlinOptions {
        freeCompilerArgs = listOf("-Xjsr305=strict")
        jvmTarget = "17"
    }
}

apply(from = "gradle/environment.gradle.kts")
val configureEnvironment = extra["configureEnvironment"] as (task: ProcessForkOptions) -> Unit

tasks.bootRun {
    val t = this
    doFirst {
        configureEnvironment(t)
    }
}