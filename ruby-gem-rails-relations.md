# rails relations

rails support 6 types

    belongs_to
    has_one
    has_many
    has_many :through
    has_one :through
    has_and_belongs_to_many

## 1:1 relation

migration file:

    def up
        create_table :photographers do |t|
            t.timestamps
        end
        create_table :curriculums do |t|
            #t.references :photographer, index: true
            t.belongs_to :photographer, { [index: true, optional: true] }
            t.timestamps
        end
    end

classes:

    class Photographer
        has_one :curriculum
    end

    class Curriculum
        belongs_to :photographer
    end

methods:

	c = Photographer.all.first.curriculum
	p = Curriculum.all.first.photographer
	Photographer.all.first.curriculum.delete


##  1:1 self references

migration file:

	def up
	  create_table :employees do |t|
	    #t.references :manager, index: true
	    t.belongs_to  :manager, index: true
	    t.timestamps
	  end
	end

classes:

    class Employee
      has_many :subordinates, {class_name: "Employee", foreign_key: "manager_id"}
			belongs_to :manager, class_name: "Employee"
    end

methods:

	e = Employee.subordinates
	m = Employee.manager
	e2 = Employee.new()
	e.subordinates << e2
	Employee.subordinates.delete(e2)

## 1:M relations

migration file:

    def up
      create_table :photographers do |t|            
          t.timestamps
      end
      create_table :photos do |t|
          t.references :photographer, index: true
          t.timestamps
      end
    end

classes:

    class Photographer
      has_many :photos
    end
		class Photo
      belongs_to :photographer
    end

methods:



## M:N relations (simple)

generate:

	rails generate CreateTableXTableYJoin 
	rails generate migration CreateColaboratorsProjectsJoin

migration file:

    def up
      create_table :projects do |t|            
          t.timestamps
      end
      create_table :colaborators do |t|          
          t.timestamps
      end
      create_table :colaborators_projects, :id => false do |t|
      	t.integer "colaborator_id"
      	t.integer "project_id"
      end
      add_index("colaborators_projects",["colaborator_id","project_id"])
    end

classes:

    class Project
      has_and_belongs_to_many :colaborators, join_table: "colaborators_projects"
    end
		class Colaborator
      has_and_belongs_to_many :projects, join_table: "colaborators_projects"
    end

methods:

	p = Project.create(...)
	me = Colaborator.create(...)
	p.colaborators << me
	p.colaborators.delete(me)
	new_project = Project.create(...)
	me.projects << new_project


## M:N relations (rich) -ments or -ships

generate:


migration_file:

	    def up
      create_table :students do |t|            
          t.timestamps
      end
      create_table :courses do |t|          
          t.timestamps
      end
      create_table :enrollments, :id => false do |t|
      	t.belongs_to "students"
      	t.belongs_to "courses"
      end
      add_index("colaborators_projects",["",""])
    end

classes:

	class Student
		has_many :enrollments
	end
	class Course
	  has_many :enrollments
	end 
	class Enrollment
		belongs_to :student
		belongs_to :course
	end

methods:




# extras

belongs_to association supports these options:

    :autosave
    :class_name
    :counter_cache
    :dependent
    :foreign_key
    :primary_key
    :inverse_of
    :polymorphic
    :touch
    :validate
    :optional
