# RAILS MIGRATIONS


	class ChangeProductsPrice < ActiveRecord::Migration[5.0]
	  def change
	    reversible do |dir|
	      change_table :products do |t|
	        dir.up   { t.change :price, :string }
	        dir.down { t.change :price, :integer }
	      end
	    end
	  end
	end

OR 

	class ChangeProductsPrice < ActiveRecord::Migration[5.0]
	  def up
	    change_table :products do |t|
	      t.change :price, :string
	    end
	  end
	 
	  def down
	    change_table :products do |t|
	      t.change :price, :integer
	    end
	  end
	end

## fields types

	change_table :products do |t|
		t.column # adds an ordinary column. Ex: t.column(:name, :string)

		t.index # adds a new index.
		t.timestamps
		t.change # changes the column definition. Ex: t.change(:name, :string, :limit => 80)
		t.change_default # changes the column default value.
		t.rename # changes the name of the column.
		t.references
		t.belongs_to
		t.string
		t.text
		t.integer
		t.float
		t.decimal
		t.datetime
		t.timestamp
		t.time
		t.date
		t.binary
		t.boolean
		t.remove
		t.remove_references
		t.remove_belongs_to
		t.remove_index
	end


	add_column :products, :part_number, :string
    add_index :products, :part_number




Creation

    create_join_table(table_1, table_2, options): Creates a join table having its name as the lexical order of the first two arguments. See ActiveRecord::ConnectionAdapters::SchemaStatements#create_join_table for details.

    create_table(name, options): Creates a table called name and makes the table object available to a block that can then add columns to it, following the same format as add_column. See example above. The options hash is for fragments like “DEFAULT CHARSET=UTF-8” that are appended to the create table definition.

    add_column(table_name, column_name, type, options): Adds a new column to the table called table_name named column_name specified to be one of the following types: :string, :text, :integer, :float, :decimal, :datetime, :timestamp, :time, :date, :binary, :boolean. A default value can be specified by passing an options hash like { default: 11 }. Other options include :limit and :null (e.g. { limit: 50, null: false }) – see ActiveRecord::ConnectionAdapters::TableDefinition#column for details.

    add_foreign_key(from_table, to_table, options): Adds a new foreign key. from_table is the table with the key column, to_table contains the referenced primary key.

    add_index(table_name, column_names, options): Adds a new index with the name of the column. Other options include :name, :unique (e.g. { name: 'users_name_index', unique: true }) and :order (e.g. { order: { name: :desc } }).

    add_reference(:table_name, :reference_name): Adds a new column reference_name_id by default an integer. See ActiveRecord::ConnectionAdapters::SchemaStatements#add_reference for details.

    add_timestamps(table_name, options): Adds timestamps (created_at and updated_at) columns to table_name.

Modification

    change_column(table_name, column_name, type, options): Changes the column to a different type using the same parameters as add_column.

    change_column_default(table_name, column_name, default_or_changes): Sets a default value for column_name defined by default_or_changes on table_name. Passing a hash containing :from and :to as default_or_changes will make this change reversible in the migration.

    change_column_null(table_name, column_name, null, default = nil): Sets or removes a +NOT NULL+ constraint on column_name. The null flag indicates whether the value can be NULL. See ActiveRecord::ConnectionAdapters::SchemaStatements#change_column_null for details.

    change_table(name, options): Allows to make column alterations to the table called name. It makes the table object available to a block that can then add/remove columns, indexes or foreign keys to it.

    rename_column(table_name, column_name, new_column_name): Renames a column but keeps the type and content.

    rename_index(table_name, old_name, new_name): Renames an index.

    rename_table(old_name, new_name): Renames the table called old_name to new_name.

Deletion

    drop_table(name): Drops the table called name.

    drop_join_table(table_1, table_2, options): Drops the join table specified by the given arguments.

    remove_column(table_name, column_name, type, options): Removes the column named column_name from the table called table_name.

    remove_columns(table_name, *column_names): Removes the given columns from the table definition.

    remove_foreign_key(from_table, options_or_to_table): Removes the given foreign key from the table called table_name.

    remove_index(table_name, column: column_names): Removes the index specified by column_names.

    remove_index(table_name, name: index_name): Removes the index specified by index_name.

    remove_reference(table_name, ref_name, options): Removes the reference(s) on table_name specified by ref_name.

    remove_timestamps(table_name, options): Removes the timestamp columns (created_at and updated_at) from the table definition.



## rails g migration "AddXXXToYYY" or "RemoveXXXFromYYY"

	rails generate migration AddPartNumberToProducts part_number:string40235974

	rails generate migration RemovePartNumberFromProducts part_number:string

## rails g migration "CreateXXX"

	rails generate migration CreateProducts name:string part_number:string

	rails generate migration AddUserRefToProducts user:references

	rails generate migration CreateJoinTableCustomerProduct customer product

## rails g migration JoinTable

	rails generate migration CreateJoinTableCustomerProduct customer product

	class CreateJoinTableCustomerProduct < ActiveRecord::Migration[5.0]
	  def change
	    create_join_table :customers, :products do |t|
	      # t.index [:customer_id, :product_id]
	      # t.index [:product_id, :customer_id]
	    end
	  end
	end

## rails g migration model

	rails generate model Product name:string description:text

	class CreateProducts < ActiveRecord::Migration[5.0]
	  def change
	    create_table :products do |t|
	      t.string :name
	      t.text :description
	 
	      t.timestamps
	    end
	  end
	end


## modifiers 

	rails generate migration AddDetailsToProducts 'price:decimal{5,2}' supplier:references{polymorphic}


##  Changing Tables

	change_table :products do |t|
	  t.remove :description, :name
	  t.string :part_number
	  t.index :part_number
	  t.rename :upccode, :upc_code
	end