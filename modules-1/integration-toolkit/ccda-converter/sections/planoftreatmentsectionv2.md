# Plan of Treatment Section (V2)

OID: 2.16.840.1.113883.10.20.22.2.10

LOINC: 18776-5

Alias: plan-of-treatment

Internal ID: PlanofTreatmentSectionV2

[IG Link](https://www.hl7.org/ccdasearch/templates/2.16.840.1.113883.10.20.22.2.10.html)

## Plan of treatment section making. [WIP]
To make Plan of treatment section we need to convert all entries from the input resources.
          
In this case we have 3 entries:
          
* Observation
          
* Encounter
          
* MedicationStatement
          
* Goal


```json
[ {
  "resourceType" : "Observation",
  "code" : {
    "coding" : [ {
      "code" : "142008000",
      "display" : "ECG",
      "system" : "http://snomed.info/sct"
    } ]
  },
  "id" : "SOME-STRING",
  "note" : [ {
    "text" : null
  } ],
  "effective" : {
    "dateTime" : "2012-10-02T00:00:00Z"
  },
  "status" : "registered",
  "subject" : {
    "id" : "patient",
    "resourceType" : "Patient"
  }
}, {
  "resourceType" : "Encounter",
  "status" : "planned",
  "meta" : {
    "profile" : [ "http://hl7.org/fhir/us/core/StructureDefinition/us-core-encounter" ]
  },
  "type" : [ {
    "coding" : [ {
      "code" : "185349003",
      "display" : "encounter for check-up (procedure)",
      "system" : "http://snomed.info/sct"
    } ]
  } ],
  "id" : "SOME-STRING",
  "class" : {
    "code" : "IMP",
    "display" : "inpatient encounter",
    "system" : "http://terminology.hl7.org/ValueSet/v3-ActEncounterCode"
  },
  "period" : {
    "start" : "2013-10-15"
  },
  "subject" : {
    "id" : "patient",
    "resourceType" : "Patient"
  }
}, {
  "resourceType" : "MedicationStatement",
  "status" : "intended",
  "medication" : {
    "CodeableConcept" : {
      "coding" : [ {
        "code" : "1191",
        "display" : "aspirin",
        "system" : "http://www.nlm.nih.gov/research/umls/rxnorm"
      } ]
    }
  },
  "id" : "SOME-STRING",
  "dosage" : [ {
    "route" : {
      "coding" : [ {
        "code" : "C38288",
        "display" : "ORAL",
        "system" : "http://ncithesaurus-stage.nci.nih.gov"
      } ]
    },
    "doseAndRate" : [ {
      "dose" : {
        "Quantity" : {
          "unit" : "milliGRAM(s)",
          "value" : 81.0
        }
      }
    } ]
  } ],
  "effective" : {
    "Period" : {
      "start" : "2012-10-02T00:00:00Z",
      "end" : "2012-10-30T23:59:00Z"
    }
  },
  "subject" : {
    "resourceType" : "Patient",
    "id" : "patient"
  }
}, {
  "description" : {
    "coding" : [ {
      "code" : "404684003",
      "display" : "http://snomed.info/sct",
      "system" : "http://terminology.hl7.org/CodeSystem/goal-priority"
    } ]
  },
  "expressedBy" : {
    "name" : [ {
      "given" : [ "Nurse" ],
      "family" : "Florence",
      "use" : "official",
      "suffix" : [ "RN" ]
    } ],
    "qualification" : [ {
      "code" : {
        "coding" : [ {
          "code" : "163W00000X",
          "display" : "Registered nurse",
          "system" : "http://hl7.org/fhir/ValueSet/provider-taxonomy"
        } ]
      }
    } ],
    "id" : "d839038b-7171-4165-a760-467925b43857",
    "resourceType" : "Practitioner"
  },
  "resourceType" : "Goal",
  "extension" : [ {
    "value" : {
      "dateTime" : "2013-07-30"
    },
    "url" : "authoring-time"
  } ],
  "priority" : {
    "coding" : [ {
      "code" : "medium-priority",
      "display" : "Medium Priority",
      "system" : "http://terminology.hl7.org/CodeSystem/goal-priority"
    } ]
  },
  "id" : "9b56c25d-9104-45ee-9fa4-e0f3afaa01c1",
  "target" : [ {
    "detail" : {
      "Range" : {
        "low" : {
          "value" : 10,
          "unit" : "%"
        },
        "high" : null
      }
    },
    "measure" : {
      "coding" : [ {
        "code" : "45735-8",
        "display" : "Weight loss",
        "system" : "http://loinc.org"
      } ]
    },
    "due" : {
      "date" : "2013-10-15"
    }
  } ],
  "subject" : {
    "resourceType" : "Patient",
    "id" : "patient"
  },
  "lifecycleStatus" : "active"
} ]
```

The section contains a list of entries converted from the input resources.
```xml
<entry>
   <observation moodCode="GOL" classCode="OBS">
      <templateId root="2.16.840.1.113883.10.20.22.4.121" extension="2022-06-01"/>
      <templateId root="2.16.840.1.113883.10.20.22.4.121"/>
      <id root="9b56c25d-9104-45ee-9fa4-e0f3afaa01c1"/>
      <code codeSystem="2.16.840.1.113883.6.1"
             codeSystemName="HTTP://LOINC.ORG"
             displayName="Weight loss"
             code="45735-8"/>
      <statusCode code="active"/>
      <effectiveTime value="20131015"/>
      <value xsi:type="IVL_PQ">
         <low value="10" unit="%"/>
      </value>
      <author>
         <templateId root="2.16.840.1.113883.10.20.22.4.119"/>
         <time value="20130730"/>
         <assignedAuthor>
            <id root="d839038b-7171-4165-a760-467925b43857"/>
            <code codeSystem="2.16.840.1.113883.6.101"
                   codeSystemName="HTTP://HL7.ORG/FHIR/VALUESET/PROVIDER-TAXONOMY"
                   displayName="Registered nurse"
                   code="163W00000X"/>
            <addr nullFlavor="UNK"/>
            <telecom nullFlavor="UNK"/>
            <assignedPerson>
               <name use="L">
                  <given>Nurse</given>
                  <family>Florence</family>
                  <suffix>RN</suffix>
               </name>
            </assignedPerson>
         </assignedAuthor>
      </author>
      <entryRelationship typeCode="REFR">
         <observation classCode="OBS" moodCode="EVN">
            <templateId root="2.16.840.1.113883.10.20.22.4.143"/>
            <id root="538eef21-036e-4e39-8771-234cd4b0893c"/>
            <code code="225773000" codeSystem="2.16.840.1.113883.6.96"/>
            <value code="394848005"
                    displayName="Medium Priority"
                    codeSystemName="SNOMED"
                    codeSystem="2.16.840.1.113883.6.96"
                    xsi:type="CD"/>
         </observation>
      </entryRelationship>
   </observation>
</entry>
```