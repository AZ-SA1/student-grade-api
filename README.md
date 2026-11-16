# Student Grade API — SE 4111 CI/CD Project

Spring Boot 3.2.0 / Java 17 / Maven / JUnit / Log4j2 / SonarQube Cloud / Docker / GitHub Actions.

These files were reconstructed from the uploaded SE 4111 CI/CD Project Guide. The final `/api/health` activity is already included.

## Before pushing to GitHub

1. Edit `pom.xml` and replace `REPLACE_WITH_SONAR_ORG` and `REPLACE_WITH_SONAR_PROJECT_KEY` with the actual SonarQube Cloud keys.
2. Create the repository `student-grade-api` in GitHub.
3. In GitHub repository **Settings > Secrets and variables > Actions**, add:
   - `SONAR_TOKEN`
   - `DOCKERHUB_USERNAME`
   - `DOCKERHUB_TOKEN`
4. Commit and push to the `main` branch to trigger `.github/workflows/ci-cd.yml`.

**Never put tokens or passwords in your source files or Git history.**

## Run locally

```bash
mvn clean test
mvn spring-boot:run
```

Open:
- http://localhost:8080/api/students
- http://localhost:8080/api/students/1
- http://localhost:8080/api/health

Example POST (curl):
```bash
curl -X POST http://localhost:8080/api/students -H 'Content-Type: application/json' -d '{"name":"Khalid","course":"SE4111","grade":91.0}'
```

## Docker

```bash
docker build -t student-grade-api:local .
docker run -d -p 8080:8080 --name grades student-grade-api:local
docker logs grades
docker stop grades
docker rm grades
```

## Notes

- Student data is held **in memory**, as in the lab guide; restarting the app resets the list.
- The original guide's two initial test scenarios and its final health-check test are included (3 tests total).
- The GET-all test checks the initial entries without assuming test execution order.
- SonarQube Cloud requires a configured project and token; Docker Hub publishing requires a configured account and token.
- This project is provided as source files; CI/CD secrets and external accounts must be configured by you.
