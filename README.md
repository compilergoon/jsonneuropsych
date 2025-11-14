# jsonneuropsych
schema for reports 
fyi schema for neuropsych report i've been using to generate reports; 
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Neuropsychological Evaluation Report",
  "type": "object",
  "required": [
    "report_metadata",
    "patient",
    "referral",
    "cognitive_complaints",
    "medical_neurological_history",
    "psychiatric_history",
    "test_results",
    "diagnostic_impressions",
    "recommendations"
  ],
  "properties": {
    "report_metadata": {
      "type": "object",
      "required": ["date_of_evaluation", "clinician_name", "setting", "report_type"],
      "properties": {
        "date_of_evaluation": { "type": "string", "format": "date" },
        "report_type": {
          "type": "string",
          "enum": ["neuropsychological_evaluation", "neurobehavioral_status_exam", "addendum", "other"]
        },
        "clinician_name": { "type": "string" },
        "clinician_credentials": { "type": "string" },
        "setting": { "type": "string" },
        "sources_of_information": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["clinical_interview", "medical_records", "collateral_informant", "self_report_measures", "neuropsych_testing", "other"]
          }
        },
        "referring_provider_copies_to": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },

    "patient": {
      "type": "object",
      "required": ["initials_or_id", "age", "gender", "education_years"],
      "properties": {
        "name": { "type": "string" },
        "initials_or_id": { "type": "string" },
        "date_of_birth": { "type": "string", "format": "date" },
        "age": { "type": "number" },
        "gender": { "type": "string" },
        "handedness": { "type": "string", "enum": ["right", "left", "mixed", "unknown"] },
        "marital_status": { "type": "string" },
        "primary_language": { "type": "string" },
        "other_languages": {
          "type": "array",
          "items": { "type": "string" }
        },
        "education_years": { "type": "number" },
        "highest_education_level": { "type": "string" },
        "occupation": { "type": "string" },
        "employer": { "type": "string" },
        "work_status": {
          "type": "string",
          "enum": ["full_time", "part_time", "disabled", "unemployed", "retired", "homemaker", "student", "other"]
        },
        "living_situation": { "type": "string" },
        "informant": {
          "type": "object",
          "properties": {
            "name": { "type": "string" },
            "relationship_to_patient": { "type": "string" },
            "cohabiting": { "type": "boolean" }
          }
        }
      }
    },

    "referral": {
      "type": "object",
      "required": ["referral_source", "reason_for_referral"],
      "properties": {
        "referral_source": {
          "type": "object",
          "properties": {
            "name": { "type": "string" },
            "discipline": { "type": "string" },
            "clinic_or_hospital": { "type": "string" }
          }
        },
        "reason_for_referral": { "type": "string" },
        "specific_referral_questions": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },

    "seizure_epilepsy_history": {
      "type": "object",
      "properties": {
        "has_seizure_disorder": { "type": "boolean" },
        "primary_neurological_diagnosis": { "type": "string" },
        "onset_date": { "type": "string", "format": "date" },
        "semiology_description": { "type": "string" },
        "nocturnal_predominant": { "type": "boolean" },
        "typical_episode_duration_minutes": { "type": "number" },
        "episode_components": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "ictal_jerking",
              "tonic_clonic",
              "vocalization",
              "sleepwalking_or_wandering",
              "unresponsiveness",
              "incontinence",
              "tongue_biting",
              "postictal_confusion",
              "injury",
              "other"
            ]
          }
        },
        "lifetime_seizure_count_estimate": { "type": "integer" },
        "seizure_frequency_course": { "type": "string" },
        "most_recent_seizure_date": { "type": "string", "format": "date" },
        "only_during_sleep_or_naps": { "type": "boolean" },
        "injuries_related_to_seizures": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "description": { "type": "string" },
              "date": { "type": "string", "format": "date" },
              "required_hospitalization": { "type": "boolean" },
              "icu_admission": { "type": "boolean" }
            }
          }
        },
        "driving_status_and_restrictions": { "type": "string" },
        "neurologist_name": { "type": "string" },
        "neurology_workup_summary": { "type": "string" },
        "eeg_findings": {
          "type": "object",
          "properties": {
            "most_recent_eeg_date": { "type": "string", "format": "date" },
            "summary": { "type": "string" },
            "lateralization_localization": { "type": "string" }
          }
        },
        "neuroimaging": {
          "type": "object",
          "properties": {
            "mri_available": { "type": "boolean" },
            "most_recent_mri_date": { "type": "string", "format": "date" },
            "most_recent_mri_site": { "type": "string" },
            "structural_findings_summary": { "type": "string" }
          }
        }
      }
    },

    "cognitive_complaints": {
      "type": "object",
      "required": ["primary_complaint"],
      "properties": {
        "primary_complaint": { "type": "string" },
        "onset_pattern": {
          "type": "string",
          "enum": ["sudden", "subacute", "gradual", "unknown"]
        },
        "approximate_onset_date": { "type": "string", "format": "date" },
        "course": {
          "type": "string",
          "enum": ["improving", "worsening", "fluctuating", "stable", "unknown"]
        },
        "domains_endorsed": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "memory",
              "attention_concentration",
              "processing_speed",
              "language",
              "executive_functions",
              "visuospatial",
              "motor_coordination",
              "other"
            ]
          }
        },
        "patient_description": { "type": "string" },
        "informant_description": { "type": "string" },
        "anosognosia_or_limited_awareness": { "type": "boolean" },
        "functional_impact": {
          "type": "object",
          "properties": {
            "work_impact": { "type": "string" },
            "home_impact": { "type": "string" },
            "safety_concerns": { "type": "string" }
          }
        }
      }
    },

    "medical_neurological_history": {
      "type": "object",
      "properties": {
        "major_medical_conditions": {
          "type": "array",
          "items": { "type": "string" }
        },
        "prior_cardiac_diagnoses": {
          "type": "array",
          "items": { "type": "string" }
        },
        "history_of_head_injury_tbi": { "type": "string" },
        "sleep_history": {
          "type": "object",
          "properties": {
            "typical_hours": { "type": "number" },
            "sleep_onset_latency": { "type": "string" },
            "nighttime_awakenings_per_night": { "type": "number" },
            "sleep_apnea_suspected_or_dx": { "type": "boolean" },
            "other_sleep_issues": { "type": "string" }
          }
        },
        "pain": {
          "type": "object",
          "properties": {
            "current_pain_presence": { "type": "boolean" },
            "description": { "type": "string" }
          }
        },
        "headaches": {
          "type": "object",
          "properties": {
            "has_headaches": { "type": "boolean" },
            "description": { "type": "string" }
          }
        },
        "dizziness_or_balance_issues": {
          "type": "object",
          "properties": {
            "dizziness_present": { "type": "boolean" },
            "description": { "type": "string" },
            "falls_unrelated_to_seizures": { "type": "string" }
          }
        },
        "vision_hearing_status": {
          "type": "object",
          "properties": {
            "vision_correction": { "type": "string" },
            "vision_issues": { "type": "string" },
            "hearing_issues": { "type": "string" }
          }
        }
      }
    },

    "psychiatric_history": {
      "type": "object",
      "properties": {
        "prior_psychiatric_diagnoses": {
          "type": "array",
          "items": { "type": "string" }
        },
        "history_of_anxiety": { "type": "string" },
        "history_of_depression": { "type": "string" },
        "onset_relative_to_neurological_symptoms": { "type": "string" },
        "prior_psychotherapy": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "modality": { "type": "string" },
              "format": { "type": "string", "enum": ["in_person", "telehealth", "group", "other"] },
              "approx_start_date": { "type": "string", "format": "date" },
              "approx_end_date": { "type": "string", "format": "date" },
              "sessions_count_estimate": { "type": "integer" },
              "perceived_benefit": { "type": "string" }
            }
          }
        },
        "prior_psychiatric_hospitalizations": { "type": "string" },
        "psychotropic_medication_history": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "class": { "type": "string" },
              "approx_dates": { "type": "string" },
              "reason_for_discontinuation": { "type": "string" }
            }
          }
        },
        "current_mood_symptoms": { "type": "string" },
        "current_anxiety_symptoms": { "type": "string" },
        "other_psych_symptoms": { "type": "string" }
      }
    },

    "substance_use_history": {
      "type": "object",
      "properties": {
        "alcohol": {
          "type": "object",
          "properties": {
            "pattern_of_use_past": { "type": "string" },
            "typical_daily_intake": { "type": "string" },
            "age_of_onset": { "type": "number" },
            "last_use_date": { "type": "string", "format": "date" },
            "period_of_abstinence_months": { "type": "number" },
            "prior_diagnoses_related_to_alcohol": {
              "type": "array",
              "items": { "type": "string" }
            },
            "formal_treatment_history": { "type": "string" }
          }
        },
        "tobacco_nicotine": { "type": "string" },
        "other_substances": { "type": "string" }
      }
    },

    "medications": {
      "type": "object",
      "properties": {
        "current_medications": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "dose_mg": { "type": "number" },
              "frequency": { "type": "string" },
              "indication": { "type": "string" },
              "prescribing_provider": { "type": "string" }
            }
          }
        },
        "recently_discontinued_medications": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "reason_for_discontinuation": { "type": "string" }
            }
          }
        },
        "medication_management_ability": { "type": "string" }
      }
    },

    "family_history": {
      "type": "object",
      "properties": {
        "neurodegenerative_disorders": {
          "type": "array",
          "items": { "type": "string" }
        },
        "movement_disorders": {
          "type": "array",
          "items": { "type": "string" }
        },
        "epilepsy_or_seizure_disorders": {
          "type": "array",
          "items": { "type": "string" }
        },
        "psychiatric_disorders": {
          "type": "array",
          "items": { "type": "string" }
        },
        "substance_use_disorders": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },

    "psychosocial_occupational": {
      "type": "object",
      "properties": {
        "developmental_history": { "type": "string" },
        "education_history": { "type": "string" },
        "learning_difficulties_or_special_ed": { "type": "string" },
        "occupational_history": { "type": "string" },
        "current_role_demands": { "type": "string" },
        "changes_in_functioning_since_onset": { "type": "string" },
        "financial_management": { "type": "string" },
        "social_supports": { "type": "string" },
        "legal_issues": { "type": "string" }
      }
    },

    "functional_status": {
      "type": "object",
      "properties": {
        "basic_adls": { "type": "string" },
        "instrumental_adls": { "type": "string" },
        "driving_status": { "type": "string" },
        "work_capacity": { "type": "string" },
        "safety_concerns": { "type": "string" }
      }
    },

    "mental_status_exam": {
      "type": "object",
      "properties": {
        "appearance_behavior": { "type": "string" },
        "speech_language": { "type": "string" },
        "mood": { "type": "string" },
        "affect": { "type": "string" },
        "thought_process": { "type": "string" },
        "thought_content": { "type": "string" },
        "perceptual_disturbances": { "type": "string" },
        "orientation": {
          "type": "object",
          "properties": {
            "person": { "type": "boolean" },
            "place": { "type": "boolean" },
            "time": { "type": "boolean" },
            "situation": { "type": "boolean" }
          }
        },
        "insight": { "type": "string" },
        "judgment": { "type": "string" },
        "test_engagement_and_effort": { "type": "string" }
      }
    },

    "test_results": {
      "type": "object",
      "properties": {
        "orientation_brief_screening": {
          "type": "object",
          "properties": {
            "date": { "type": "string", "format": "date" },
            "description": { "type": "string" },
            "score_summary": { "type": "string" }
          }
        },
        "attention_working_memory": {
          "type": "string"
        },
        "serial_subtraction_performance": {
          "type": "object",
          "properties": {
            "task_type": { "type": "string" },
            "total_trials": { "type": "integer" },
            "correct": { "type": "integer" },
            "error_pattern": { "type": "string" }
          }
        },
        "memory_measures": {
          "type": "string"
        },
        "other_neuropsych_tests": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "test_name": { "type": "string" },
              "cognitive_domain": { "type": "string" },
              "raw_score": { "type": "number" },
              "scaled_or_t_score": { "type": "number" },
              "percentile": { "type": "number" },
              "qualitative_description": { "type": "string" }
            }
          }
        },
        "self_report_scales": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "scale_name": { "type": "string" },
              "score": { "type": "number" },
              "interpretive_range": { "type": "string" }
            }
          }
        }
      }
    },

    "risk_assessment": {
      "type": "object",
      "properties": {
        "suicidal_ideation_current": { "type": "string" },
        "suicidal_ideation_past": { "type": "string" },
        "homicidal_ideation": { "type": "string" },
        "self_harm_behaviors": { "type": "string" },
        "violence_risk": { "type": "string" },
        "protective_factors": { "type": "string" }
      }
    },

    "diagnostic_impressions": {
      "type": "object",
      "required": ["neurocognitive_diagnoses", "psychiatric_diagnoses"],
      "properties": {
        "neurocognitive_diagnoses": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "diagnosis": { "type": "string" },
              "icd_or_dsm_code": { "type": "string" },
              "level_of_certainty": { "type": "string" }
            }
          }
        },
        "psychiatric_diagnoses": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "diagnosis": { "type": "string" },
              "icd_or_dsm_code": { "type": "string" },
              "level_of_certainty": { "type": "string" }
            }
          }
        },
        "medical_diagnoses_relevant_to_cognition": {
          "type": "array",
          "items": { "type": "string" }
        },
        "rule_out_or_consider": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },

    "case_formulation": {
      "type": "object",
      "properties": {
        "summary_of_findings": { "type": "string" },
        "contribution_of_neurological_factors": { "type": "string" },
        "contribution_of_psychiatric_factors": { "type": "string" },
        "contribution_of_substance_use": { "type": "string" },
        "psychosocial_context": { "type": "string" },
        "prognosis": { "type": "string" }
      }
    },

    "recommendations": {
      "type": "object",
      "required": ["summary"],
      "properties": {
        "summary": { "type": "string" },
        "medical_followup": {
          "type": "array",
          "items": { "type": "string" }
        },
        "neurology_specific": {
          "type": "array",
          "items": { "type": "string" }
        },
        "psychotherapy_or_psychiatry": {
          "type": "array",
          "items": { "type": "string" }
        },
        "cognitive_rehabilitation_or_compensatory_strategies": {
          "type": "array",
          "items": { "type": "string" }
        },
        "safety_and_risk_management": {
          "type": "array",
          "items": { "type": "string" }
        },
        "work_and_driving": {
          "type": "array",
          "items": { "type": "string" }
        },
        "lifestyle_and_health_behaviors": {
          "type": "array",
          "items": { "type": "string" }
        },
        "family_education_and_support": {
          "type": "array",
          "items": { "type": "string" }
        },
        "additional_testing_or_monitoring": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    }
  }
}
