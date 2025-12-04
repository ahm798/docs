# Gov360 Organization Service API Endpoints


## . Module Catalog (Tree View)

### Get Complete Module Catalog
```
GET /module-catalog
```

**Response:**
```json
[
  {
    "publicId": "b2c3d4e5-f6g7-8901-bcde-f12345678901",
    "name": {
      "en": "Planning and Execution",
      "ar": "التخطيط والتنفيذ"
    },
    "description": {
      "en": "Strategic planning and performance execution modules",
      "ar": "وحدات التخطيط الاستراتيجي وتنفيذ الأداء"
    },
    "modules": [
      {
        "publicId": "d4e5f6g7-h8i9-0123-defg-234567890123",
        "name": {
          "en": "Strategic Management",
          "ar": "الإدارة الاستراتيجية"
        },
        "description": {
          "en": "Strategic planning, goals, and KPI management",
          "ar": "التخطيط الاستراتيجي وإدارة الأهداف ومؤشرات الأداء"
        }
      },
      {
        "publicId": "e5f6g7h8-i9j0-1234-efgh-345678901234",
        "name": {
          "en": "Operational Planning",
          "ar": "التخطيط التشغيلي"
        },
        "description": {
          "en": "Operational plans and execution tracking",
          "ar": "الخطط التشغيلية وتتبع التنفيذ"
        }
      }
    ]
  },
  {
    "publicId": "c3d4e5f6-g7h8-9012-cdef-123456789012",
    "name": {
      "en": "Compliance",
      "ar": "الإلتزام"
    },
    "description": {
      "en": "Regulatory compliance and governance modules",
      "ar": "وحدات الإلتزام التنظيمي والحوكمة"
    },
    "modules": [
      {
        "publicId": "f6g7h8i9-j0k1-2345-fghi-456789012345",
        "name": {
          "en": "Risk Management",
          "ar": "إدارة المخاطر"
        },
        "description": {
          "en": "Enterprise risk assessment and mitigation",
          "ar": "تقييم وتخفيف المخاطر المؤسسية"
        }
      }
    ]
  }
]
```




## Base URL
```
http://localhost:36010/api/organization
```


---

## . Organizations

### 1.1 List All Organizations
```
GET /organizations
POST /organizations
PATCH /organizations/{id}
PUT /organizations/{id}
PUT /organizations/{id}
```

**Response:**
```json
{
  "_embedded": {
    "organizations": [
      {
        "createdAt": "2025-12-04T10:00:00Z",
        "createdBy": "SYSTEM",
        "lastModifiedAt": "2025-12-04T10:00:00Z",
        "lastModifiedBy": "SYSTEM",
        "deletedAt": null,
        "deletedBy": null,
        "publicId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
        "slug": "ministry-health",
        "name": {
          "en": "Ministry of Health",
          "ar": "وزارة الصحة"
        },
        "_links": {
          "self": {
            "href": "http://localhost:36010/api/organization/organizations/1"
          }
        }
      },
      {
        "createdAt": "2025-12-04T10:00:00Z",
        "createdBy": "SYSTEM",
        "lastModifiedAt": "2025-12-04T10:00:00Z",
        "lastModifiedBy": "SYSTEM",
        "deletedAt": null,
        "deletedBy": null,
        "publicId": "b2c3d4e5-f6g7-8901-bcde-f12345678901",
        "slug": "ministry-education",
        "name": {
          "en": "Ministry of Education",
          "ar": "وزارة التعليم"
        },
        "_links": {
          "self": {
            "href": "http://localhost:36010/api/organization/organizations/2"
          }
        }
      }
    ]
  },
  "_links": {
    "self": {
      "href": "http://localhost:36010/api/organization/organizations"
    }
  },
  "page": {
    "size": 20,
    "totalElements": 5,
    "totalPages": 1,
    "number": 0
  }
}
```

## 2. Module Groups

### List All Module Groups
```
GET /module-groups
POST /module-groups
GET /module-groups/{id}
DELETE /module-groups/{id}
PATCH /module-groups/{id}
```

**Response:**
```json
{
  "_embedded": {
    "moduleGroups": [
      {
        "createdAt": "2025-12-04T10:00:00Z",
        "createdBy": "SYSTEM",
        "lastModifiedAt": "2025-12-04T10:00:00Z",
        "lastModifiedBy": "SYSTEM",
        "deletedAt": null,
        "deletedBy": null,
        "publicId": "b2c3d4e5-f6g7-8901-bcde-f12345678901",
        "name": {
          "en": "Planning and Execution",
          "ar": "التخطيط والتنفيذ"
        },
        "description": {
          "en": "Strategic planning and performance execution modules",
          "ar": "وحدات التخطيط الاستراتيجي وتنفيذ الأداء"
        },
        "_links": {
          "self": {
            "href": "http://localhost:36010/api/organization/module-groups/1"
          },
          "modules": {
            "href": "http://localhost:36010/api/organization/module-groups/1/modules"
          }
        }
      }
    ]
  },
  "page": {
    "size": 20,
    "totalElements": 4,
    "totalPages": 1,
    "number": 0
  }
}
```


## 3. Modules

### List All Modules
```
GET /modules
GET /modules
put /modules/{id}
patch /modules/{id}
delete /modules/{id}
GET /modules/{id}
```

**Response:**
```json
{
  "_embedded": {
    "modules": [
      {
        "createdAt": "2025-12-04T10:00:00Z",
        "createdBy": "SYSTEM",
        "lastModifiedAt": "2025-12-04T10:00:00Z",
        "lastModifiedBy": "SYSTEM",
        "deletedAt": null,
        "deletedBy": null,
        "publicId": "d4e5f6g7-h8i9-0123-defg-234567890123",
        "name": {
          "en": "Strategic Management",
          "ar": "الإدارة الاستراتيجية"
        },
        "description": {
          "en": "Strategic planning, goals, and KPI management",
          "ar": "التخطيط الاستراتيجي وإدارة الأهداف ومؤشرات الأداء"
        },
        "_links": {
          "self": {
            "href": "http://localhost:36010/api/organization/modules/1"
          },
          "moduleGroup": {
            "href": "http://localhost:36010/api/organization/modules/1/moduleGroup"
          }
        }
      }
    ]
  },
  "page": {
    "size": 20,
    "totalElements": 14,
    "totalPages": 1,
    "number": 0
  }
}
```

