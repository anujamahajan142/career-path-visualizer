# -----------------------------------------------------------
# Career Path Visualizer Based on Your Skills - Terminal App
# Author: Anuja Mahajan (or your name here)
# Description:
#     This program helps users discover potential career paths
#     based on their current skills and suggests what to learn.
# -----------------------------------------------------------

import time

# -------------------------
# Function to show welcome message
# -------------------------
def welcome():
    print("=" * 60)
    print("           🎯 CAREER PATH VISUALIZER 🎯")
    print("=" * 60)
    print("This tool helps you discover careers based on your current skills.")
    print("Just type your known skills and we’ll recommend matching roles!\n")
    time.sleep(1)

# -------------------------
# Career and skills dataset (you can expand this!)
# -------------------------
career_data = {
    "Data Scientist": ["Python", "Pandas", "SQL", "Machine Learning"],
    "Web Developer": ["HTML", "CSS", "JavaScript", "Python"],
    "Data Analyst": ["Python", "Excel", "SQL", "Data Visualization"],
    "AI Engineer": ["Python", "TensorFlow", "Deep Learning", "ML"],
    "Digital Marketer": ["SEO", "Content Writing", "Analytics", "Social Media"],
    "Mobile App Developer": ["Java", "Kotlin", "Android Studio", "UI Design"],
    "Cybersecurity Analyst": ["Networking", "Linux", "Cryptography", "Firewalls"],
    "Cloud Engineer": ["AWS", "Docker", "Kubernetes", "DevOps"],
    "UI/UX Designer": ["Figma", "Wireframing", "Prototyping", "User Research"]
}

# -------------------------
# Function to analyze skills and recommend careers
# -------------------------
def analyze_skills(user_skills):
    results = []
    for career, required_skills in career_data.items():
        required = [skill.lower() for skill in required_skills]
        matched = set(user_skills) & set(required)
        missing = set(required) - set(user_skills)

        match_percent = int(len(matched) / len(required) * 100)

        if matched:
            results.append({
                "career": career,
                "match": matched,
                "missing": missing,
                "percent": match_percent
            })
    return results

# -------------------------
# Function to display results
# -------------------------
def display_results(results):
    if not results:
        print("\n❌ Sorry! No careers matched your current skills.")
        print("Tip: Try adding more technical or common industry skills.\n")
        return

    print("\n🔍 Based on your skills, here are the best-matching career paths:\n")

    for res in sorted(results, key=lambda x: x["percent"], reverse=True):
        print(f"💼 Career: {res['career']}")
        print(f"✅ Matched Skills: {', '.join(res['match'])}")
        print(f"📚 Skills to Learn: {', '.join(res['missing'])}")
        print(f"🔢 Match Percentage: {res['percent']}%")
        print("-" * 50)
        time.sleep(0.5)

# -------------------------
# Function to save results to file
# -------------------------
def save_results_to_file(results, user_skills):
    with open("career_suggestions.txt", "w") as f:
        f.write("Career Suggestions Based on Your Skills\n")
        f.write("=" * 45 + "\n")
        f.write(f"Your Skills: {', '.join(user_skills)}\n\n")

        for res in sorted(results, key=lambda x: x["percent"], reverse=True):
            f.write(f"Career: {res['career']}\n")
            f.write(f"Matched Skills: {', '.join(res['match'])}\n")
            f.write(f"Skills to Learn: {', '.join(res['missing'])}\n")
            f.write(f"Match %: {res['percent']}%\n")
            f.write("-" * 45 + "\n")

    print("\n📝 Results saved to 'career_suggestions.txt' successfully!")

# -------------------------
# Main Program Execution
# -------------------------
def main():
    welcome()

    user_input = input("👉 Enter your skills (comma separated): ")
    user_skills = [skill.strip().lower() for skill in user_input.split(",")]

    print("\n⏳ Analyzing your skills, please wait...\n")
    time.sleep(1.5)

    results = analyze_skills(user_skills)
    display_results(results)

    if results:
        save = input("\n💾 Do you want to save these results to a file? (yes/no): ").lower()
        if save == "yes":
            save_results_to_file(results, user_skills)
        else:
            print("👍 Okay, results not saved.")

    print("\n✅ Thank you for using Career Path Visualizer! All the best! 🚀")

# Run the app
if __name__ == "__main__":
    main()
