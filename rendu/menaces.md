# Rapport d'Audit de Sécurité - API Bibliothèque Symfony

## **Démarche Adoptée**

### **1. Modélisation des Menaces (STRIDE)**

Application de la méthode STRIDE pour identifier les vulnérabilités spécifiques au contexte d'une bibliothèque :

| **Type de Menace**         | **Exemple Identifié**       | **Contre-mesure**                 |
| -------------------------- | --------------------------- | --------------------------------- |
| **Spoofing**               | Usurpation de token JWT     | Tokens signés + expiration courte |
| **Tampering**              | Injection SQL via recherche | ORM Doctrine + validation         |
| **Repudiation**            | Déni d'emprunt              | Logs détaillés avec audit trail   |
| **Information Disclosure** | Accès aux emprunts d'autrui | Contrôle de propriété des données |
| **Denial of Service**      | Spam sur endpoints          | Rate limiting Symfony             |
| **Elevation of Privilege** | Accès admin non autorisé    | Annotations de rôles strictes     |

### **2. Pipeline CI/CD Sécurisé**

Implémentation d'un pipeline GitHub Actions avec 5 étapes de contrôle :

1. **Analyse SAST** (Semgrep) - Détection de vulnérabilités dans le code source
2. **Audit des dépendances** (Composer) - Vérification des CVE connues
3. **Security Check Symfony** - Contrôle spécifique au framework
4. **Scan DAST** (OWASP ZAP) - Tests de sécurité dynamiques sur l'application

## **Résultats Obtenus**

### **Tests de Sécurité Réussis**

- **59 contrôles PASSÉS** sans vulnérabilité critique
- **0 échec** de sécurité majeur
- **Aucune CVE** détectée dans les dépendances

### **Améliorations Identifiées**

- 7 avertissements mineurs (headers sécuritaires manquants)
- Configuration CSP à ajouter pour protection XSS
- Optimisation des en-têtes de réponse HTTP
