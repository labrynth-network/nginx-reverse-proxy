# nginx-reverse-proxy

Repository for managing Nginx reverse proxy configurations as code.

## Reverse Proxy Configuration

This repository serves as the source of truth for internal and external Nginx reverse proxy configurations, which can then easily be deployed to proxy hosts through CI/CD workflows.

## Repository Structure

```
├── internal/
│   ├── nginx.conf
│   └── conf.d/
│       ├── production/
│    	│   ├── app1/
│   	│   │   └── app1.prod.conf
│   	│   └── app2/
│   	│       └── app2.prod.conf
│       └── development/
└── external/
```

- Configurations are organized into `internal/` and `external/` based on which proxy they are for
- Each proxy configuration is organized by environment and application (Ex: `production/app1/`)
- The actual reverse proxy configuration resides in `<app-name>.<environment>.conf`

## Standards & Best Practices

The following standards should be adhered to wherever possible:

- Persist TLS through the full connection (Client --- HTTPS ---> Proxy --- HTTPS ---> Backend Server Pool) wherever possible, as is recommended in a zero-trust environment
- <u>Always</u> redirect HTTP traffic to HTTPS traffic in proxy configurations
- Use source IP `allow` and `deny` rules in internal proxy configs based on expected sources, as it is harder to implement network access control with Nginx due to every endpoint being served on the same IP
