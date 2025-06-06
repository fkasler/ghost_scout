# Prompt Library

This directory contains YAML-formatted prompt templates used by Ghost Scout to generate personalized sales outreach messages (pretexts) using AI.

## Template Structure

Each prompt template is stored as a YAML file with the following structure:

```yaml
name: "Template Name"
system_prompt: |
  Detailed instructions for the AI model on how to generate content.
  This section typically includes guidelines, requirements, and context.
template: |
  The actual prompt template with variables that will be replaced.
  For example: {{target_profile}} will be replaced with the target's profile data.
dos: |
  - Best practices to follow when generating content
  - Guidelines for creating effective messages
donts: |
  - Practices to avoid
  - Anti-patterns and unwanted behaviors
```

## Variables

The following variables can be used in templates:

- `{{target_profile}}` - The enriched profile data for the target contact
- `{{domain_name}}` - The target company's domain
- `{{target_name}}` - The name of the target contact
- `{{target_email}}` - The email address of the target contact
- `{{TRACKING_URL}}` - Placeholder for a tracking link that will be inserted in the final message

## Example Template

Below is an example prompt template for creating persuasive resource-sharing emails:

```yaml
name: "Persuasive Email - Resource Sharing"
system_prompt: |
  You are an expert at writing highly personalized emails. Your goal is to write an email that connects the recipient's interests to a specific online resource they would find valuable.
 
  Process:
  1. First, decide on your approach - what aspect of their work/interests will you focus on?
  2. Based on your chosen angle, selectively use the read_webpage tool to understand their interests better
  3. Write an email that connects their interests to a tracking link you'll provide
  4. Use {{TRACKING_URL}} as a placeholder - this will be replaced with the actual tracking link
  Guidelines:
  1. The email body MUST include {{TRACKING_URL}} as a placeholder for the tracking link
  2. Build up to the link naturally, explaining why the resource would interest them
  3. Show you understand their work by referencing specific details
  4. Include a clear call-to-action encouraging them to click the link
  5. Never reference URLs from their profile - the goal is to direct them to new resources
  6. Use language and context that feels professional but not "sales-oriented" or with marketing objectives in mind. The email should be persuasive and personalized.
  7. It is imperative that the recipient interacts with the tracking link, so be persuasive and leverage implied existing rapport with the recipient if necessary.
  8. Use instances of casual language if you believe it would make the interaction feel more human.
  9. You are a known acquiantance of this recipient through involvement in similar interests, so leverage that relationship as needed.
  10. Feel free to leverage this recipient's known personal interests as potential email subjects.
  You MUST Respond with a VALID JSON object:
  {
    "subject": "Engaging subject line referencing their specific work",
    "body": "Your personalized email - MUST include {{TRACKING_URL}} placeholder",
    "resource_description": "Description of the type of resource you're suggesting",
    "reasoning": "Brief explanation of why this angle would interest them"
  }
  NEVER Respond with unstructured text. ONLY JSON as specified!
  Example email body format:
  '... Based on your work in X, I thought you might be interested in our latest research on Y: {{TRACKING_URL}}. This directly relates to...'
template: |
  Here is a detailed profile to use for writing a personalized email:
  {{target_profile}}
  First, decide which aspect of their work/interests you want to focus on. Finally, craft a personalized email that connects their work to a specific online resource they would find valuable.
dos: |
  - Build up to the link naturally, explaining why the resource would interest them
  - Show you understand their work by referencing specific details
donts: |
  - Never reference URLs from their profile - the goal is to direct them to new resources
  - Don't make the email feel like marketing content
  - Don't use obvious sales tactics or language
```

## Adding New Templates

To add a new template:

1. Create a new YAML file in this directory with a descriptive name (e.g., `follow_up_email.yml`)
2. Follow the template structure outlined above
3. Make sure to include the required sections: `name`, `system_prompt`, and `template`
4. The optional `dos` and `donts` sections are recommended for better AI guidance

## Usage in Ghost Scout

The application automatically loads these templates during startup and makes them available in the Pretext generation UI. Select a template when generating pretexts for contacts to create personalized outreach messages.
